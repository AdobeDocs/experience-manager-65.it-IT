---
title: Rendering di Forms as HTML
seo-title: Rendering Forms as HTML
description: Utilizza il servizio Forms per eseguire il rendering dei moduli come HTML in risposta a una richiesta HTTP da parte di un browser web. È possibile utilizzare l’API Java e l’API di servizio Web per eseguire il rendering dei moduli come HTML.
seo-description: Use the Forms service to render forms as HTML in response to an HTTP request from a web browser. You can use the Java API and Web Service API to render forms as HTML.
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
role: Developer
exl-id: e6887e45-a472-41d4-9620-c56fd5b72b4c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4150'
ht-degree: 1%

---

# Rendering di Forms as HTML {#rendering-forms-as-html}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

Il servizio Forms esegue il rendering dei moduli come HTML in risposta a una richiesta HTTP da parte di un browser Web. Un vantaggio del rendering di un modulo come HTML è dato dal fatto che il computer in cui si trova il browser Web client non richiede Adobe Reader, Acrobat o Flash Player (per le guide dei moduli (obsoleto)).

Per eseguire il rendering di un modulo come HTML, è necessario salvare la struttura del modulo come file XDP. Non è possibile eseguire il rendering di una struttura del modulo salvata come file PDF come HTML. Quando si sviluppa una struttura del modulo in Designer di cui sarà eseguito il rendering come HTML, tenere in considerazione i seguenti criteri:

* Non utilizzare le proprietà relative al bordo degli oggetti per disegnare righe, riquadri o griglie all’interno del modulo. In alcuni browser i bordi non vengono allineati esattamente come nell’anteprima di Gli oggetti possono risultare sovrapposti o impedire di visualizzare altri oggetti nella posizione prevista.
* Potete utilizzare linee, rettangoli e cerchi per definire lo sfondo.
* Disegna testo leggermente più grande di quello che sembra necessario per contenere il testo. Alcuni browser web non visualizzano il testo in modo leggibile.

>[!NOTE]
>
>Quando si esegue il rendering di un modulo che contiene immagini di TIFF utilizzando `FormServiceClient` dell’oggetto `(Deprecated) renderHTMLForm` e `renderHTMLForm2` , le immagini di TIFF non sono visibili nel modulo HTML di cui è stato eseguito il rendering visualizzato nei browser Internet Explorer o Mozilla Firefox. Questi browser non forniscono supporto nativo per le immagini TIFF.

## Pagine HTML {#html-pages}

Quando si esegue il rendering di una struttura del modulo come modulo HTML, ogni sottomodulo di secondo livello viene rappresentato come una pagina (pannello) di HTML. In Designer è possibile visualizzare la gerarchia di un sottomodulo. I sottomoduli secondari che appartengono al sottomodulo principale (il nome predefinito di un sottomodulo principale è modulo1) sono i sottomoduli del pannello. L’esempio seguente mostra i sottomoduli della struttura del modulo.

```java
     form1
         Master Pages
         PanelSubform1
             NestedDynamicSubform
                 TextEdit1
         PanelSubform2
             TextEdit1
         PanelSubform3
             TextEdit1
         PanelSubform4
             TextEdit1
```

Quando si esegue il rendering delle strutture del modulo come moduli di HTML, i pannelli non sono vincolati a particolari dimensioni di pagina. Se si dispone di sottomoduli dinamici, questi devono essere nidificati all’interno del sottomodulo del pannello. I sottomoduli dinamici sono in grado di espandersi fino a un numero infinito di pagine HTML.

Quando si esegue il rendering di un modulo come modulo HTML, le dimensioni di pagina (necessarie per l’impaginazione dei moduli di cui è stato eseguito il rendering in PDF) non hanno alcun significato. Poiché un modulo con layout scorrevole può espandersi fino a un numero infinito di pagine di HTML, è importante evitare che i piè di pagina siano presenti nella pagina master. Un piè di pagina sotto l’area contenuto di una pagina master può sovrascrivere il contenuto di HTML che scorre oltre il limite di una pagina.

È necessario passare esplicitamente da un pannello all’altro utilizzando `xfa.host.pageUp` e `xfa.host.pageDown` metodi. È possibile modificare le pagine inviando un modulo al servizio Forms e facendo sì che il servizio Forms esegua il rendering del modulo sul dispositivo client, in genere un browser web.

>[!NOTE]
>
>Il processo di invio di un modulo al servizio Forms e successivo rendering del modulo sul dispositivo client viene definito come ciclo di trasferimento dei dati al server.

>[!NOTE]
>
>Per personalizzare l’aspetto del pulsante Firma digitale di HTML in un modulo HTML, è necessario modificare le seguenti proprietà nel file fscdigsig.css (all’interno del file adobe-forms-ds.ear > adobe-forms-ds.war ):

**.fsc-ds-ssb**: Questo foglio di stile è applicabile nel caso di un campo di firma vuoto.

**.fsc-ds-ssv**: Questo foglio di stile è applicabile nel caso di un campo di firma valido.

**.fsc-ds-ssc**: Questo foglio di stile è applicabile in caso di un campo di firma valido ma i dati sono cambiati.

**.fsc-ds-ssi**: Questo foglio di stile è applicabile in caso di campo di firma non valido.

**.fsc-ds-popup-bg**: Questa proprietà del foglio di stile non viene utilizzata.

**.fsc-ds-popup-btn**: Questa proprietà del foglio di stile non viene utilizzata.

## Script in esecuzione {#running-scripts}

Un autore di moduli specifica se uno script viene eseguito sul server o sul client. Il servizio Forms crea un ambiente di elaborazione degli eventi distribuito per l’esecuzione di informazioni sui moduli che possono essere distribuite tra il client e il server utilizzando il `runAt` attributo. Per informazioni su questo attributo o sulla creazione di script all’interno delle strutture del modulo, consultare [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Il servizio Forms può eseguire script durante il rendering del modulo. Di conseguenza, è possibile precompilare un modulo con i dati effettuando la connessione a un database o a servizi Web che potrebbero non essere disponibili sul client. Puoi anche impostare un pulsante `Click` da eseguire sul server in modo che il client possa eseguire un ciclo dei dati al server. Questo consente al client di eseguire script che possono richiedere risorse server, ad esempio un database aziendale, mentre un utente interagisce con un modulo. Per i moduli HTML, gli script formcalc possono essere eseguiti solo sul server. Di conseguenza, è necessario contrassegnare questi script per l&#39;esecuzione in `server` o `both`.

È possibile creare moduli che si spostano tra le pagine (pannelli) chiamando `xfa.host.pageUp` e `xfa.host.pageDown` metodi. Questo script è posizionato in un pulsante `Click` e `runAt` attributo impostato su `Both`. Il motivo per cui scegli `Both` è in modo che Adobe Reader o Acrobat (per i moduli di cui viene eseguito il rendering come PDF) possano modificare le pagine senza passare al server; inoltre, i moduli HTML possono modificare le pagine arrotondando i dati di attivazione al server. In altre parole, un modulo viene inviato al servizio Forms e viene eseguito il rendering di un modulo come HTML con la nuova pagina visualizzata.

È consigliabile non assegnare alle variabili di script e ai campi modulo gli stessi nomi, ad esempio item. Alcuni browser Web, come Internet Explorer, potrebbero non inizializzare una variabile con lo stesso nome di un campo modulo che si verifica un errore di script. È buona prassi assegnare nomi diversi ai campi del modulo e alle variabili di script.

Quando si esegue il rendering di moduli di HTML contenenti sia funzionalità di navigazione delle pagine che script di moduli (ad esempio, si supponga che uno script recuperi dati di campo da un database ogni volta che viene eseguito il rendering del modulo), assicurarsi che lo script del modulo si trovi nell’evento form:calculate anziché in form:readyevent.

Gli script di modulo che si trovano nell’evento form:ready vengono eseguiti una sola volta durante il rendering iniziale del modulo e non vengono eseguiti per i recuperi successivi della pagina. Al contrario, l&#39;evento form:calculate viene eseguito per ogni navigazione di pagina in cui viene eseguito il rendering del modulo.

>[!NOTE]
In un modulo multipagina, le modifiche apportate da JavaScript a una pagina non vengono mantenute se si passa a una pagina diversa.

È possibile richiamare script personalizzati prima di inviare un modulo. Questa funzione funziona su tutti i browser disponibili. Tuttavia, può essere utilizzato solo quando gli utenti eseguono il rendering del modulo HTML che lo contiene `Output Type` proprietà impostata su `Form Body`. Non funzionerà quando `Output Type` è `Full HTML`. Per i passaggi necessari per configurare questa funzione, consulta Configurazione di moduli nella guida di amministrazione .

È innanzitutto necessario definire una funzione di callback chiamata prima di inviare il modulo, dove si trova il nome della funzione `_user_onsubmit`. Si presume che la funzione non generi alcuna eccezione, o che, in caso contrario, l&#39;eccezione venga ignorata. Si consiglia di posizionare la funzione JavaScript nella sezione head dell’html; tuttavia, è possibile dichiararlo in qualsiasi punto prima della fine dei tag script che includono `xfasubset.js`.

Quando formserver esegue il rendering di un file XDP contenente un elenco a discesa, oltre a creare l’elenco a discesa, crea anche due campi di testo nascosti. Questi campi di testo memorizzano i dati dell’elenco a discesa (uno memorizza il nome visualizzato delle opzioni e l’altro memorizza il valore delle opzioni). Pertanto, ogni volta che un utente invia il modulo, vengono inviati tutti i dati dell’elenco a discesa. Presupponendo che non si desideri inviare così tanti dati ogni volta, è possibile scrivere uno script personalizzato per disabilitarlo. Ad esempio: Il nome dell’elenco a discesa è `drpOrderedByStateProv` e viene racchiuso nell’intestazione del sottomodulo. Il nome dell’elemento di input di HTML sarà `header[0].drpOrderedByStateProv[0]`. Il nome dei campi nascosti che memorizzano e inviano i dati del menu a discesa ha i seguenti nomi: `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

Se non desideri inviare i dati, puoi disattivare questi elementi di input nel modo seguente. `var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

```java
header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]
```

```java
var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature
    function _user_onsubmit() {
    var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]");
    elems[0].disabled = true;
    elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]");
    elems[0].disabled = true;
    }
```

## Sottoinsiemi XFA {#xfa-subsets}

Durante la creazione di strutture del modulo per il rendering come HTML, è necessario limitare lo script al sottoinsieme XFA per gli script nel linguaggio JavaScript.

Gli script eseguiti sul client o eseguiti sia sul client che sul server devono essere scritti all’interno del sottoinsieme XFA. Gli script eseguiti sul server possono utilizzare il modello di script XFA completo e FormCalc. Per informazioni sull&#39;utilizzo di JavaScript, vedi [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Quando si eseguono script sul client, solo il pannello corrente visualizzato può utilizzare script; ad esempio, non è possibile eseguire script rispetto ai campi che si trovano nel pannello A quando viene visualizzato il pannello B. Quando si eseguono script sul server, è possibile accedere a tutti i pannelli.

È inoltre necessario prestare attenzione quando si utilizzano espressioni SOM (Scripting Object Model) all&#39;interno di script eseguiti sul client. Solo un sottoinsieme semplificato di espressioni SOM è supportato da script eseguiti sul client.

## Tempistiche degli eventi {#event-timing}

Il sottoinsieme XFA definisce gli eventi XFA mappati su eventi HTML. C&#39;è una leggera differenza di comportamento nella tempistica degli eventi di calcolo e convalida. In un browser Web, viene eseguito un evento calculate completo quando si esce da un campo. Gli eventi di calcolo non vengono eseguiti automaticamente quando si apporta una modifica al valore di un campo. È possibile forzare un evento calculate chiamando la variabile `xfa.form.execCalculate` metodo .

In un browser Web, gli eventi di convalida vengono eseguiti solo all’uscita da un campo o all’invio di un modulo. È possibile forzare un evento di convalida utilizzando `xfa.form.execValidate` metodo .

Forms visualizzato in un browser Web (a differenza di Adobe Reader o Acrobat) è conforme al test null XFA (errori o avvisi) per i campi obbligatori.

* Se il test nullo genera un errore e si esce da un campo senza specificare un valore, viene visualizzata una finestra di messaggio che consente di riposizionare il campo dopo aver fatto clic su OK.
* Se un test nullo genera un avviso e si esce da un campo senza specificare un valore, viene richiesto di fare clic su OK o Annulla, in modo da poter procedere senza specificare un valore o tornare al campo per immettere un valore.

Per ulteriori informazioni su un test null, consulta [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Pulsanti modulo {#form-buttons}

Facendo clic su un pulsante di invio i dati del modulo vengono inviati al servizio Forms e viene indicata la fine dell’elaborazione del modulo. La `preSubmit` può essere impostato per l&#39;esecuzione sul client o sul server. La `preSubmit` viene eseguito prima dell’invio del modulo se è configurato per l’esecuzione sul client. In caso contrario, la `preSubmit` viene eseguito sul server durante l’invio del modulo. Per ulteriori informazioni sulla `preSubmit` evento, vedi [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Se a un pulsante non è associato alcuno script sul lato client, i dati vengono inviati al server, i calcoli vengono eseguiti sul server e il modulo HTML viene rigenerato. Se un pulsante contiene uno script sul lato client, i dati non vengono inviati al server e lo script sul lato client viene eseguito nel browser Web.

## Browser Web HTML 4.0 {#html-4-0-web-browser}

Un browser web che supporta solo HTML 4.0 non può supportare il modello di script lato client del sottoinsieme XFA. Durante la creazione di una struttura del modulo per il funzionamento sia in HTML 4.0 che in MSDHTML o CSS2HTML, uno script contrassegnato per l’esecuzione sul client viene eseguito sul server. Ad esempio, si supponga che un utente faccia clic su un pulsante posizionato in un modulo visualizzato in un browser Web HTML 4.0. In questa situazione, i dati del modulo vengono inviati al server in cui viene eseguito lo script sul lato client.

È consigliabile inserire la logica del modulo negli eventi calculate eseguiti sul server in HTML 4.0 e sul client per MSDHTML o CSS2HTML.

## Manutenzione delle modifiche alle presentazioni {#maintaining-presentation-changes}

Quando ci si sposta tra le pagine di HTML (pannelli), viene mantenuto solo lo stato dei dati. Le impostazioni come il colore di sfondo o le impostazioni obbligatorie dei campi non vengono mantenute (se diverse dalle impostazioni iniziali). Per mantenere lo stato della presentazione, è necessario creare campi (solitamente nascosti) che rappresentano lo stato della presentazione dei campi. Se si aggiunge uno script a un campo `Calculate` evento che modifica la presentazione in base ai valori dei campi nascosti, è possibile mantenere lo stato della presentazione mentre ci si sposta avanti e indietro tra le pagine di HTML (pannelli).

Lo script seguente mantiene `fillColor` di un campo basato sul valore di `hiddenField`. Supponiamo che questo script si trovi nella posizione di un campo `Calculate` evento.

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
Gli oggetti statici non vengono visualizzati in un modulo di HTML sottoposto a rendering quando nidificati all’interno di una cella di tabella. Ad esempio, un cerchio e un rettangolo nidificati all’interno di una cella di tabella non vengono visualizzati all’interno di un modulo di rendering HTML. Tuttavia, questi stessi oggetti statici vengono visualizzati correttamente quando si trovano all’esterno della tabella.

## Firma digitale dei moduli di HTML {#digitally-signing-html-forms}

Non è possibile firmare un modulo HTML che contiene un campo firma digitale se il modulo viene rappresentato come una delle seguenti trasformazioni di HTML:

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

Per informazioni sulla firma digitale di un documento, vedere [Firma digitale e certificazione dei documenti](/help/forms/developing/digitally-signing-certifying-documents.md)

## Rendering di un modulo XHTML conforme alle linee guida per l’accessibilità {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

È possibile eseguire il rendering di un modulo HTML completo conforme alle linee guida per l’accessibilità. In altre parole, viene eseguito il rendering del modulo all’interno di tag HTML completi, anziché all’interno di tag corpo (non in una pagina HTML completa).

## Convalida dei dati del modulo {#validating-form-data}

È consigliabile limitare l’uso delle regole di convalida per i campi modulo durante il rendering del modulo come modulo HTML. Alcune regole di convalida potrebbero non essere supportate per i moduli HTML. Ad esempio, quando un pattern di convalida di MM-GG-AAAA viene applicato a un `Date/Time` campo che si trova in una struttura del modulo di cui è eseguito il rendering come modulo HTML, non funziona correttamente, anche se la data è digitata correttamente. Tuttavia, questo pattern di convalida funziona correttamente per i moduli sottoposti a rendering come PDF.

>[!NOTE]
Per ulteriori informazioni sul servizio Forms, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo HTML, procedere come segue:

1. Includi file di progetto.
1. Creare un oggetto API client Forms.
1. Impostare le opzioni di runtime di HTML.
1. Eseguire il rendering di un modulo HTML.
1. Scrivere il flusso di dati del modulo sul browser Web client.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client Forms**

Prima di poter importare i dati in modo programmatico in un’API client di PDF, è necessario creare un client del servizio di integrazione dei dati di modulo. Quando crei un client di servizio, definisci le impostazioni di connessione necessarie per richiamare un servizio.

**Impostare le opzioni di runtime di HTML**

È possibile impostare le opzioni di esecuzione di HTML durante il rendering di un modulo HTML. Ad esempio, è possibile aggiungere una barra degli strumenti a un modulo HTML per consentire agli utenti di selezionare file allegati presenti nel computer client o di recuperare file allegati di cui è stato eseguito il rendering con il modulo HTML. Per impostazione predefinita, una barra degli strumenti di HTML è disabilitata. Per aggiungere una barra degli strumenti a un modulo HTML, è necessario impostare in modo programmatico le opzioni di esecuzione. Per impostazione predefinita, una barra degli strumenti di HTML è composta dai seguenti pulsanti:

* `Home`: Fornisce un collegamento alla radice web dell&#39;applicazione.
* `Upload`: Fornisce un&#39;interfaccia utente per selezionare i file da allegare al modulo corrente.
* `Download`: Fornisce un&#39;interfaccia utente per visualizzare i file allegati.

Quando in un modulo HTML viene visualizzata una barra degli strumenti di HTML, è possibile selezionare un massimo di dieci file da inviare insieme ai dati del modulo. Una volta inviati i file, il servizio Forms può recuperare i file.

Quando si esegue il rendering di un modulo come HTML, è possibile specificare un valore agente utente. Un valore agente utente fornisce informazioni sul browser e sul sistema. Si tratta di un valore facoltativo e puoi passare un valore di stringa vuoto. Il rapido avvio del rendering di un modulo HTML tramite l’API Java illustra come ottenere il valore di un agente utente e utilizzarlo per il rendering di un modulo come HTML.

Gli URL HTTP a cui vengono inviati i dati del modulo possono essere specificati impostando l’URL di destinazione utilizzando l’API client di Forms Service oppure possono essere specificati nel pulsante Invia contenuto nella struttura del modulo XDP. Se l’URL di destinazione è specificato nella struttura del modulo, non impostare un valore utilizzando l’API client di Forms Service.

>[!NOTE]
Il rendering di un modulo HTML con una barra degli strumenti è facoltativo.

>[!NOTE]
Se si esegue il rendering di un modulo AHTML, si consiglia di non aggiungere al modulo una barra degli strumenti.

**Rendering di un modulo HTML**

Per eseguire il rendering di un modulo HTML, è necessario specificare una struttura del modulo creata in Designer e salvata come file XDP. È inoltre necessario selezionare un tipo di trasformazione HTML. Ad esempio, è possibile specificare il tipo di trasformazione HTML che esegue il rendering di un HTML dinamico per Internet Explorer 5.0 o versione successiva.

Il rendering di un modulo HTML richiede anche valori, ad esempio valori URI necessari per il rendering di altri tipi di modulo.

**Scrivere il flusso di dati del modulo sul browser Web client**

Quando il servizio Forms esegue il rendering di un modulo HTML, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web client. Quando viene scritto nel browser Web del client, il modulo HTML è visibile all’utente.

**Consulta anche**

[Eseguire il rendering di un modulo come HTML utilizzando l’API Java](#render-a-form-as-html-using-the-java-api)

[Eseguire il rendering di un modulo come HTML utilizzando l’API del servizio Web](#render-a-form-as-html-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendering di HTML Forms con barre degli strumenti personalizzate](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Eseguire il rendering di un modulo come HTML utilizzando l’API Java {#render-a-form-as-html-using-the-java-api}

Eseguire il rendering di un modulo HTML utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Forms

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `FormsServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Impostare le opzioni di runtime di HTML

   * Crea un `HTMLRenderSpec` utilizzando il relativo costruttore.
   * Per eseguire il rendering di un modulo HTML con una barra degli strumenti, richiamare `HTMLRenderSpec` dell’oggetto `setHTMLToolbar` e passare un `HTMLToolbar` valore enum. Ad esempio, per visualizzare una barra degli strumenti verticale di HTML, passare `HTMLToolbar.Vertical`.
   * Per impostare il valore delle impostazioni internazionali del modulo HTML, richiamare l’ `HTMLRenderSpec` dell’oggetto `setLocale` e passare un valore stringa che specifica il valore delle impostazioni internazionali. (Questa è un’impostazione opzionale.)
   * Per eseguire il rendering del modulo HTML all’interno di tag HTML completi, richiamare `HTMLRenderSpec` dell’oggetto `setOutputType` metodo e passaggio `OutputType.FullHTMLTags`. (Questa è un’impostazione opzionale.)

   >[!NOTE]
   Forms non viene riprodotto correttamente in HTML quando il `StandAlone` opzione `true` e `ApplicationWebRoot` fa riferimento a un server diverso da J2EE application server che ospita AEM Forms (il `ApplicationWebRoot` viene specificato utilizzando `URLSpec` oggetto passato al `FormsServiceClient` dell’oggetto `(Deprecated) renderHTMLForm` metodo). Quando il `ApplicationWebRoot` è un altro server di quello che ospita AEM Forms, il valore dell’URI web root nella console di amministrazione deve essere impostato come valore URI dell’applicazione web Form. Per eseguire questa operazione, accedi alla console di amministrazione, fai clic su Servizi > Forms e imposta l’URI della directory principale web come https://server-name:port/FormServer. Quindi, salva le impostazioni.

1. Rendering di un modulo HTML

   Richiama il `FormsServiceClient` dell’oggetto `(Deprecated) renderHTMLForm` e passare i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, verificare di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valore enum che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con Dynamic HTML per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` oggetto contenente i dati da unire al modulo. Se non si desidera unire i dati, passare un valore vuoto `com.adobe.idp.Document` oggetto.
   * La `HTMLRenderSpec` oggetto che memorizza le opzioni di runtime di HTML.
   * Un valore stringa che specifica la variabile `HTTP_USER_AGENT` valore di intestazione; ad esempio, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` oggetto che memorizza i valori URI necessari per eseguire il rendering di un modulo HTML.
   * A `java.util.HashMap` oggetto che memorizza gli allegati di file. Si tratta di un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   La `(Deprecated) renderHTMLForm` restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo che può essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Crea un `com.adobe.idp.Document` richiamando l&#39;oggetto `FormsResult` oggetto ‘s `getOutputContent` metodo .
   * Ottieni il tipo di contenuto del `com.adobe.idp.Document` richiamandone l&#39;oggetto `getContentType` metodo .
   * Imposta la `javax.servlet.http.HttpServletResponse` tipo di contenuto dell’oggetto richiamandone il tipo `setContentType` e passare il tipo di contenuto `com.adobe.idp.Document` oggetto.
   * Crea un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il `javax.servlet.http.HttpServletResponse` dell’oggetto `getOutputStream` metodo .
   * Crea un `java.io.InputStream` richiamando l&#39;oggetto `com.adobe.idp.Document` dell’oggetto `getInputStream` metodo .
   * Creare un array di byte e compilarlo con il flusso di dati del modulo richiamando il `InputStream` dell’oggetto `read` e passare l&#39;array di byte come argomento.
   * Richiama il `javax.servlet.ServletOutputStream` dell’oggetto `write` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al `write` metodo .

**Consulta anche**

[Rendering di Forms as HTML](#rendering-forms-as-html)

[Avvio rapido (modalità SOAP): Rendering di un modulo HTML utilizzando l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eseguire il rendering di un modulo come HTML utilizzando l’API del servizio Web {#render-a-form-as-html-using-the-web-service-api}

Eseguire il rendering di un modulo HTML utilizzando l’API Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client Forms

   Crea un `FormsService` e impostare i valori di autenticazione.

1. Impostare le opzioni di runtime di HTML

   * Crea un `HTMLRenderSpec` utilizzando il relativo costruttore.
   * Per eseguire il rendering di un modulo HTML con una barra degli strumenti, richiamare `HTMLRenderSpec` dell’oggetto `setHTMLToolbar` e passare un `HTMLToolbar` valore enum. Ad esempio, per visualizzare una barra degli strumenti verticale di HTML, passare `HTMLToolbar.Vertical`.
   * Per impostare il valore delle impostazioni internazionali del modulo HTML, richiamare l’ `HTMLRenderSpec` dell’oggetto `setLocale` e passare un valore stringa che specifica il valore delle impostazioni internazionali. Per ulteriori informazioni, consulta [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Per eseguire il rendering del modulo HTML all’interno di tag HTML completi, richiamare `HTMLRenderSpec` dell’oggetto `setOutputType` metodo e passaggio `OutputType.FullHTMLTags`.

   >[!NOTE]
   Forms non viene riprodotto correttamente in HTML quando il `StandAlone` opzione `true` e `ApplicationWebRoot` fa riferimento a un server diverso da J2EE application server che ospita AEM Forms (il `ApplicationWebRoot` viene specificato utilizzando `URLSpec` oggetto passato al `FormsServiceClient` dell’oggetto `(Deprecated) renderHTMLForm` metodo). Quando il `ApplicationWebRoot` è un altro server di quello che ospita AEM Forms, il valore dell’URI web root nella console di amministrazione deve essere impostato come valore URI dell’applicazione web Form. Per eseguire questa operazione, accedi alla console di amministrazione, fai clic su Servizi > Forms e imposta l’URI della directory principale web come https://server-name:port/FormServer. Quindi, salva le impostazioni.

1. Rendering di un modulo HTML

   Richiama il `FormsService` dell’oggetto `(Deprecated) renderHTMLForm` e passare i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, verificare di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valore enum che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con Dynamic HTML per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * A `BLOB` oggetto contenente i dati da unire al modulo. Se non si desidera unire i dati, passare `null`. (Vedi [Precompilazione di Forms con layout fluidi](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts).)
   * La `HTMLRenderSpec` oggetto che memorizza le opzioni di runtime di HTML.
   * Un valore stringa che specifica la variabile `HTTP_USER_AGENT` valore di intestazione; ad esempio, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Se non si desidera impostare questo valore, è possibile passare una stringa vuota.
   * A `URLSpec` oggetto che memorizza i valori URI necessari per eseguire il rendering di un modulo HTML. (Vedi [Specificare i valori URI](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * A `java.util.HashMap` oggetto che memorizza gli allegati di file. Si tratta di un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo. (Vedi [Allegare file al modulo](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * Un vuoto `com.adobe.idp.services.holders.BLOBHolder` oggetto popolato dal metodo . Questo valore del parametro memorizza il modulo di cui è stato effettuato il rendering.
   * Un vuoto `com.adobe.idp.services.holders.BLOBHolder` oggetto popolato dal metodo . Questo parametro memorizzerà i dati XML di output.
   * Un vuoto `javax.xml.rpc.holders.LongHolder` oggetto popolato dal metodo . Questo argomento memorizza il numero di pagine nel modulo.
   * Un vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato dal metodo . Questo argomento memorizza il valore delle impostazioni internazionali.
   * Un vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato dal metodo . Questo argomento memorizza il valore di rendering di HTML utilizzato.
   * Un vuoto `com.adobe.idp.services.holders.FormsResultHolder` oggetto che conterrà i risultati dell&#39;operazione.

   La `(Deprecated) renderHTMLForm` popola il `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come ultimo valore argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Crea un `FormResult` ottenendo il valore del `com.adobe.idp.services.holders.FormsResultHolder` dell’oggetto `value` membro dati.
   * Crea un `BLOB` oggetto che contiene i dati del modulo richiamando il `FormsResult` dell’oggetto `getOutputContent` metodo .
   * Ottieni il tipo di contenuto del `BLOB` richiamandone l&#39;oggetto `getContentType` metodo .
   * Imposta la `javax.servlet.http.HttpServletResponse` tipo di contenuto dell’oggetto richiamandone il tipo `setContentType` e passare il tipo di contenuto `BLOB` oggetto.
   * Crea un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il `javax.servlet.http.HttpServletResponse` dell’oggetto `getOutputStream` metodo .
   * Creare un array di byte e compilarlo richiamando il `BLOB` dell’oggetto `getBinaryData` metodo . Questa attività assegna il contenuto del `FormsResult` all&#39;array di byte.
   * Richiama il `javax.servlet.http.HttpServletResponse` dell’oggetto `write` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al `write` metodo .

**Consulta anche**

[Rendering di Forms as HTML](#rendering-forms-as-html)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
