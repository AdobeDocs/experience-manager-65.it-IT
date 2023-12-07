---
title: Rendering di Forms come HTML
description: Utilizza il servizio Forms per eseguire il rendering dei moduli come HTML in risposta a una richiesta HTTP da un browser web. Puoi utilizzare l’API Java e l’API Web Service per eseguire il rendering dei moduli come HTML.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: e6887e45-a472-41d4-9620-c56fd5b72b4c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '4102'
ht-degree: 0%

---

# Rendering di Forms come HTML {#rendering-forms-as-html}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

Il servizio Forms esegue il rendering dei moduli come HTML in risposta a una richiesta HTTP da un browser web. Un vantaggio del rendering di un modulo come HTML è che il computer in cui si trova il browser web client non richiede Adobe Reader, Acrobat o Flash Player (per le guide dei moduli, è obsoleto).

Per eseguire il rendering di un modulo come HTML, è necessario salvare la struttura del modulo come file XDP. Non è possibile eseguire il rendering come HTML di una struttura di modulo salvata come file PDF. Durante lo sviluppo di una progettazione di moduli in Designer che verrà sottoposta a rendering come HTML, considera i seguenti criteri:

* Non utilizzare le proprietà del bordo di un oggetto per disegnare linee, caselle o griglie nel modulo. Alcuni browser potrebbero non allineare i bordi esattamente come appaiono in un&#39;anteprima. Gli oggetti possono apparire sovrapposti o allontanare altri oggetti dalla posizione prevista.
* È possibile utilizzare linee, rettangoli e cerchi per definire lo sfondo.
* Disegna un testo leggermente più grande di quello che sembra necessario per contenere il testo. Alcuni browser web non visualizzano il testo in modo leggibile.

>[!NOTE]
>
>Quando si esegue il rendering di un modulo contenente immagini TIFF utilizzando `FormServiceClient` dell&#39;oggetto `(Deprecated) renderHTMLForm` e `renderHTMLForm2` metodi, le immagini TIFF non sono visibili nel modulo HTML di cui è stato eseguito il rendering e che viene visualizzato in Internet Explorer o Mozilla Firefox. Questi browser non forniscono il supporto nativo per le immagini TIFF.

## Pagine HTML {#html-pages}

Quando si esegue il rendering di una struttura di modulo come modulo HTML, ogni sottomaschera di secondo livello viene riprodotto come pagina HTML (pannello). È possibile visualizzare la gerarchia di una sottomaschera in Designer. Le sottomaschere secondarie che appartengono alla sottomaschera principale (il nome predefinito di una sottomaschera principale è form1) sono le sottomaschere del pannello. Nell&#39;esempio seguente vengono illustrate le sottomaschere di una struttura di maschera.

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

Quando le progettazioni dei moduli vengono sottoposte a rendering come moduli HTML, i pannelli non sono vincolati a una particolare dimensione di pagina. Se disponi di sottomaschere dinamiche, queste devono essere nidificate all’interno della sottomaschera del pannello. Le sottomaschere dinamiche possono espandersi fino a un numero infinito di pagine HTML.

Quando un modulo viene renderizzato come modulo HTML, le dimensioni della pagina (necessarie per impaginare i moduli renderizzati come PDF) non hanno alcun significato. Poiché un modulo con un layout scorrevole può essere espanso fino a un numero infinito di pagine HTML, è importante evitare i piè di pagina nella pagina master. Un piè di pagina sotto l&#39;area del contenuto di una pagina master può sovrascrivere il contenuto HTML che passa oltre il limite di una pagina.

È necessario passare esplicitamente da un pannello all’altro utilizzando `xfa.host.pageUp` e `xfa.host.pageDown` metodi. Per modificare le pagine, è necessario inviare un modulo al servizio Forms e fare in modo che il servizio Forms esegua nuovamente il rendering del modulo sul dispositivo client, in genere un browser Web.

>[!NOTE]
>
>Il processo di invio di un modulo al servizio Forms e successivo rendering del modulo sul dispositivo client da parte del servizio Forms viene definito round tripping data to the server (dati di round tripping).

>[!NOTE]
>
>Se si desidera personalizzare l&#39;aspetto del pulsante Firma digitale HTML in un modulo HTML, è necessario modificare le seguenti proprietà nel file fscdigsig.css (all&#39;interno del file adobe-forms-ds.ear > adobe-forms-ds.war ):

**.fsc-ds-ssb**: questo foglio di stile è applicabile se è presente un campo del segno vuoto.

**.fsc-ds-ssv**: questo foglio di stile è applicabile se è presente un campo Segno valido.

**.fsc-ds-ssc**: questo foglio di stile è applicabile se è presente un campo Segno valido ma i dati sono stati modificati.

**.fsc-ds-ssi**: questo foglio di stile è applicabile se è presente un campo del segno non valido.

**.fsc-ds-popup-bg**: questa proprietà del foglio di stile non viene utilizzata.

**.fsc-ds-popup-btn**: questa proprietà del foglio di stile non viene utilizzata.

## Esecuzione degli script {#running-scripts}

Un autore di moduli specifica se uno script viene eseguito sul server o sul client. Il servizio Forms crea un ambiente di elaborazione degli eventi distribuito per l&#39;esecuzione di informazioni sui moduli che può essere distribuito tra il client e il server utilizzando `runAt` attributo. Per informazioni su questo attributo o sulla creazione di script nelle progettazioni di moduli, vedere [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Il servizio Forms può eseguire script durante il rendering del modulo. Di conseguenza, è possibile precompilare un modulo con i dati connettendosi a un database o a servizi Web che potrebbero non essere disponibili sul client. È inoltre possibile impostare i `Click` da eseguire sul server in modo che il client esegua il round trip dei dati al server. Questo consente al client di eseguire script che potrebbero richiedere risorse server, ad esempio un database aziendale, mentre un utente interagisce con un modulo. Per i moduli HTML, gli script formcalc possono essere eseguiti solo sul server. Di conseguenza, è necessario contrassegnare questi script per l&#39;esecuzione alle `server` o `both`.

È possibile progettare moduli che si spostano tra pagine (pannelli) chiamando `xfa.host.pageUp` e `xfa.host.pageDown` metodi. Questo script viene inserito nel `Click` evento e `runAt` attributo impostato su `Both`. Il motivo scelto `Both` è in modo che Adobe Reader o Acrobat (per i moduli di cui è stato eseguito il rendering come PDF) possano modificare le pagine senza passare al server e che HTML forms possa modificare le pagine arrotondando i dati al server. In altre parole, un modulo viene inviato al servizio Forms e un modulo viene riprodotto come HTML con la nuova pagina visualizzata.

È consigliabile non assegnare alle variabili di script e ai campi modulo gli stessi nomi, ad esempio item. Alcuni browser Web, ad esempio Internet Explorer, potrebbero non inizializzare una variabile con lo stesso nome di un campo modulo, causando un errore di script. È buona prassi assegnare nomi diversi ai campi modulo e alle variabili di script.

Quando si esegue il rendering di moduli HTML che contengono sia funzionalità di spostamento tra pagine che script di moduli (ad esempio, si supponga che uno script recuperi i dati di campo da un database ogni volta che viene eseguito il rendering del modulo), assicurarsi che lo script del modulo si trovi nell&#39;evento form:calculal posto del form:readyevent.

Gli script di modulo presenti nell&#39;evento form:ready vengono eseguiti una sola volta durante il rendering iniziale del modulo e non vengono eseguiti per i recuperi di pagina successivi. Al contrario, l’evento form:calculate viene eseguito per ogni navigazione della pagina in cui viene eseguito il rendering del modulo.

>[!NOTE]
>
In un modulo multipagina, le modifiche apportate da JavaScript a una pagina non vengono mantenute se si passa a un&#39;altra pagina.

È possibile richiamare script personalizzati prima di inviare un modulo. Questa funzione funziona su tutti i browser disponibili. Tuttavia, può essere utilizzato solo quando gli utenti eseguono il rendering del modulo HTML con `Output Type` proprietà impostata su `Form Body`. Non funzionerà quando `Output Type` è `Full HTML`. Per informazioni su come configurare questa funzione, consulta Configurazione dei moduli nella guida per l’amministrazione.

Definire innanzitutto una funzione di callback chiamata prima dell&#39;invio del modulo, in cui il nome della funzione è `_user_onsubmit`. Si presume che la funzione non genererà alcuna eccezione o, in caso contrario, l’eccezione verrà ignorata. Si consiglia di posizionare la funzione JavaScript nella sezione head dell’html; tuttavia, è possibile dichiararla ovunque prima della fine dei tag script che includono `xfasubset.js`.

Quando formserver esegue il rendering di un XDP che contiene un elenco a discesa, oltre a creare l’elenco a discesa, crea anche due campi di testo nascosti. Questi campi di testo memorizzano i dati dell’elenco a discesa (uno memorizza il nome visualizzato delle opzioni, l’altro il valore delle opzioni). Pertanto, ogni volta che un utente invia il modulo, vengono inviati tutti i dati dell’elenco a discesa. Supponendo di non voler inviare tutti quei dati ogni volta, puoi scrivere uno script personalizzato per disabilitarlo. Ad esempio: il nome dell’elenco a discesa è `drpOrderedByStateProv` e viene racchiuso nell’intestazione del sottomodulo. Il nome dell’elemento di input HTML sarà `header[0].drpOrderedByStateProv[0]`. Il nome dei campi nascosti che memorizzano e inviano i dati del menu a discesa ha i seguenti nomi: `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

Se non desideri pubblicare i dati, puoi disattivare questi elementi di input nel modo seguente. `var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

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

Durante la creazione di progettazioni di moduli da riprodurre come HTML, è necessario limitare gli script al sottoinsieme XFA per gli script in linguaggio JavaScript.

Gli script eseguiti sul client o sia sul client che sul server devono essere scritti all&#39;interno del sottoinsieme XFA. Gli script eseguiti sul server possono utilizzare il modello di script XFA completo e anche FormCalc. Per informazioni sull’utilizzo di JavaScript, consulta [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Quando si eseguono gli script sul client, solo il pannello corrente visualizzato può utilizzare gli script; ad esempio, non è possibile eseguire script per i campi presenti nel pannello A quando viene visualizzato il pannello B. Durante l’esecuzione di script sul server, è possibile accedere a tutti i pannelli.

Prestare attenzione quando si utilizzano espressioni SOM (Scripting Object Model) all&#39;interno di script eseguiti sul client. Solo un sottoinsieme semplificato di espressioni SOM è supportato dagli script eseguiti sul client.

## Tempistica eventi {#event-timing}

Il sottoinsieme XFA definisce gli eventi XFA mappati agli eventi HTML. C’è una leggera differenza di comportamento nella tempistica degli eventi di calcolo e convalida. In un browser web, un evento di calcolo completo viene eseguito quando esci da un campo. Gli eventi di calcolo non vengono eseguiti automaticamente quando si apporta una modifica al valore di un campo. È possibile forzare un evento di calcolo chiamando il `xfa.form.execCalculate` metodo.

In un browser web, gli eventi di convalida vengono eseguiti solo quando si esce da un campo o si invia un modulo. Puoi forzare un evento di convalida utilizzando `xfa.form.execValidate` metodo.

I Forms visualizzati in un browser web (al contrario di Adobe Reader o Acrobat) sono conformi al test null XFA (errori o avvertenze) per i campi obbligatori.

* Se il test null genera un errore e si esce da un campo senza specificare un valore, viene visualizzata una finestra di messaggio e si viene riposizionati nel campo dopo aver fatto clic su OK.
* Se un test null genera un avviso e si esce da un campo senza specificare un valore, viene richiesto di fare clic su OK o su Annulla per poter procedere senza specificare un valore o tornare al campo per immettere un valore.

Per ulteriori informazioni su un test null, vedere [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Pulsanti modulo {#form-buttons}

Facendo clic su un pulsante Invia, i dati del modulo vengono inviati al servizio Forms e rappresentano la fine dell’elaborazione del modulo. Il `preSubmit` può essere impostato per l&#39;esecuzione sul client o sul server. Il `preSubmit` viene eseguito prima dell’invio del modulo se è configurato per essere eseguito sul client. In caso contrario, `preSubmit` viene eseguito sul server durante l’invio del modulo. Per ulteriori informazioni su `preSubmit` evento, vedi [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Se a un pulsante non è associato alcuno script sul lato client, i dati vengono inviati al server, i calcoli vengono eseguiti sul server e il modulo HTML viene rigenerato. Se un pulsante contiene uno script lato client, i dati non vengono inviati al server e lo script lato client viene eseguito nel browser Web.

## Browser web HTML 4.0 {#html-4-0-web-browser}

Un browser Web che supporta solo HTML 4.0 non può supportare il modello di script lato client del sottoinsieme XFA. Durante la creazione di una struttura di modulo da utilizzare sia in HTML 4.0 che in MSDHTML o CSS2HTML, uno script contrassegnato per l&#39;esecuzione sul client verrà effettivamente eseguito sul server. Si supponga, ad esempio, che un utente faccia clic su un pulsante che si trova in un modulo visualizzato in un browser Web di HTML 4.0. In questa situazione, i dati del modulo vengono inviati al server in cui viene eseguito lo script lato client.

È consigliabile inserire la logica del modulo negli eventi di calcolo, che vengono eseguiti nel server di HTML 4.0 e nel client di MSDHTML o CSS2HTML.

## Gestione delle modifiche alla presentazione {#maintaining-presentation-changes}

Quando ci si sposta tra pagine HTML (pannelli), viene mantenuto solo lo stato dei dati. Impostazioni quali il colore di sfondo o le impostazioni obbligatorie dei campi non vengono mantenute (se diverse dalle impostazioni iniziali). Per mantenere lo stato di presentazione, è necessario creare campi, in genere nascosti, che rappresentano lo stato di presentazione dei campi. Se aggiungi uno script al di un campo `Calculate` evento che modifica la presentazione in base ai valori dei campi nascosti, è possibile mantenere lo stato della presentazione mentre ci si sposta avanti e indietro tra le pagine HTML (pannelli).

Lo script seguente mantiene `fillColor` di un campo in base al valore di `hiddenField`. Supponiamo che questo script si trovi nel `Calculate` evento.

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
>
Gli oggetti statici non vengono visualizzati in un modulo di rendering HTML quando sono nidificati all&#39;interno di una cella di tabella. Ad esempio, un cerchio e un rettangolo nidificati all’interno di una cella di tabella non vengono visualizzati all’interno di un modulo di rendering HTML. Tuttavia, questi stessi oggetti statici vengono visualizzati correttamente quando si trovano all’esterno della tabella.

## Firma digitale di moduli HTML {#digitally-signing-html-forms}

Non è possibile firmare un modulo HTML contenente un campo di firma digitale se il modulo viene sottoposto a rendering come una delle seguenti trasformazioni di HTML:

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

Per informazioni sulla firma digitale di un documento, vedere [Firma digitale e certificazione dei documenti](/help/forms/developing/digitally-signing-certifying-documents.md)

## Rendering di un modulo XHTML conforme alle linee guida di accessibilità {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

È possibile eseguire il rendering di un modulo HTML completo conforme alle linee guida per l&#39;accessibilità. In altre parole, il rendering del modulo viene eseguito all’interno di tag HTML completi, mentre il rendering del modulo HTML viene eseguito all’interno di tag body (non una pagina HTML completa).

## Convalida dei dati del modulo {#validating-form-data}

È consigliabile limitare l&#39;utilizzo delle regole di convalida per i campi modulo durante il rendering del modulo come modulo HTML. Alcune regole di convalida potrebbero non essere supportate per i moduli HTML. Ad esempio, quando un pattern di convalida MM-GG-AAAA viene applicato a un `Date/Time` che si trova in una struttura di modulo di cui è stato eseguito il rendering come modulo HTML, non funziona correttamente, anche se la data è stata digitata correttamente. Tuttavia, questo modello di convalida funziona correttamente per i moduli renderizzati come PDF.

>[!NOTE]
>
Per ulteriori informazioni sul servizio Forms, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo HTML, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API client di Forms.
1. Impostare le opzioni di runtime di HTML.
1. Eseguire il rendering di un modulo HTML.
1. Scrivere il flusso di dati del modulo nel browser Web client.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Forms**

Prima di poter importare i dati a livello di programmazione in un’API formClient di PDF, è necessario creare un client del servizio di integrazione dei dati dei moduli. Quando si crea un client di servizio, vengono definite le impostazioni di connessione necessarie per richiamare un servizio.

**Imposta opzioni runtime di HTML**

È possibile impostare le opzioni di runtime di HTML durante il rendering di un modulo di HTML. È possibile, ad esempio, aggiungere una barra degli strumenti a un modulo di HTML per consentire agli utenti di selezionare i file allegati presenti nel computer client o di recuperare i file allegati di cui è stato eseguito il rendering con il modulo di HTML. Per impostazione predefinita, la barra degli strumenti di HTML è disabilitata. Per aggiungere una barra degli strumenti a un modulo di HTML, è necessario impostare le opzioni di runtime a livello di programmazione. Per impostazione predefinita, una barra degli strumenti di HTML è costituita dai pulsanti riportati di seguito.

* `Home`: fornisce un collegamento alla directory principale del web dell’applicazione.
* `Upload`: fornisce un&#39;interfaccia utente per selezionare i file da allegare al modulo corrente.
* `Download`: fornisce un’interfaccia utente per visualizzare i file allegati.

Quando in un modulo di HTML HTML viene visualizzata una barra degli strumenti, l’utente può selezionare un massimo di dieci file da inviare insieme ai dati del modulo. Una volta inviati i file, il servizio Forms può recuperarli.

Quando si esegue il rendering di un modulo come HTML, è possibile specificare un valore user-agent. Un valore user-agent fornisce informazioni sul browser e sul sistema. Questo è un valore facoltativo e puoi trasmettere un valore stringa vuoto. Il modulo Rendering di un HTML utilizzando l’avvio rapido API Java mostra come ottenere un valore agente utente e utilizzarlo per eseguire il rendering di un modulo come HTML.

Gli URL HTTP in cui vengono pubblicati i dati del modulo possono essere specificati impostando l’URL di destinazione utilizzando l’API client del servizio Forms oppure possono essere specificati nel pulsante Invia contenuto nella progettazione del modulo XDP. Se l’URL di destinazione è specificato nella progettazione del modulo, non impostare un valore utilizzando l’API client del servizio Forms.

>[!NOTE]
>
Il rendering di un modulo HTML con una barra degli strumenti è facoltativo.

>[!NOTE]
>
Se si esegue il rendering di un modulo HTML, si consiglia di non aggiungere una barra degli strumenti al modulo.

**Rendering di un modulo HTML**

Per eseguire il rendering di un modulo di HTML, specificare una struttura di modulo creata in Designer e salvata come file XDP. Selezionare un tipo di trasformazione HTML. È ad esempio possibile specificare il tipo di trasformazione HTML che esegue il rendering di un HTML dinamico per Internet Explorer 5.0 o versione successiva.

Il rendering di un modulo HTML richiede anche valori, ad esempio valori URI necessari per il rendering di altri tipi di modulo.

**Scrivere il flusso di dati del modulo nel browser Web client**

Quando il servizio Forms esegue il rendering di un modulo HTML, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web client. Quando viene scritto nel browser Web del client, il modulo HTML è visibile all&#39;utente.

**Consulta anche**

[Eseguire il rendering di un modulo come HTML utilizzando l’API Java](#render-a-form-as-html-using-the-java-api)

[Eseguire il rendering di un modulo come HTML utilizzando l’API del servizio web](#render-a-form-as-html-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva all’API di servizio Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering dei PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendering di HTML Forms con barre degli strumenti personalizzate](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Eseguire il rendering di un modulo come HTML utilizzando l’API Java {#render-a-form-as-html-using-the-java-api}

Eseguire il rendering di un modulo HTML utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi i file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client di Forms

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `FormsServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Imposta opzioni runtime di HTML

   * Creare un `HTMLRenderSpec` mediante il costruttore.
   * Per eseguire il rendering di un modulo HTML con una barra degli strumenti, richiamare `HTMLRenderSpec` dell&#39;oggetto `setHTMLToolbar` e passa un `HTMLToolbar` valore enum. Ad esempio, per visualizzare una barra degli strumenti HTML verticale, passare `HTMLToolbar.Vertical`.
   * Per impostare il valore locale per il modulo HTML, richiamare `HTMLRenderSpec` dell&#39;oggetto `setLocale` e passa un valore stringa che specifica il valore locale. (Impostazione facoltativa).
   * Per eseguire il rendering del modulo HTML all’interno di tag HTML completi, richiama `HTMLRenderSpec` dell&#39;oggetto `setOutputType` metodo e passaggio `OutputType.FullHTMLTags`. (Impostazione facoltativa).

   >[!NOTE]
   >
   Il rendering di Forms in HTML non viene eseguito correttamente quando `StandAlone` l&#39;opzione è `true` e `ApplicationWebRoot` fa riferimento a un server diverso dal server applicazioni J2EE che ospita AEM Forms (il `ApplicationWebRoot` il valore viene specificato utilizzando `URLSpec` oggetto passato al `FormsServiceClient` dell&#39;oggetto `(Deprecated) renderHTMLForm` metodo). Quando `ApplicationWebRoot` è un altro server di quello che ospita AEM Forms, il valore dell’URI della radice web nella console di amministrazione deve essere impostato come valore dell’URI dell’applicazione web del modulo. Per eseguire questa operazione, accedi alla console di amministrazione, fai clic su Servizi > Forms e imposta l’URI della directory principale del web come https://server-name:port/FormServer. Quindi, salva le impostazioni.

1. Rendering di un modulo HTML

   Richiama `FormsServiceClient` dell&#39;oggetto `(Deprecated) renderHTMLForm` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura di modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valore enum che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo di HTML compatibile con dynamic HTML per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` oggetto contenente dati da unire con il modulo. Se non desideri unire i dati, passa un campo vuoto `com.adobe.idp.Document` oggetto.
   * Il `HTMLRenderSpec` oggetto che memorizza le opzioni di runtime di HTML.
   * Un valore stringa che specifica il `HTTP_USER_AGENT` valore intestazione; ad esempio, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` oggetto che memorizza i valori URI necessari per il rendering di un modulo HTML.
   * A `java.util.HashMap` oggetto che memorizza gli allegati. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera allegare file al modulo.

   Il `(Deprecated) renderHTMLForm` il metodo restituisce un `FormsResult` oggetto contenente un flusso di dati modulo che può essere scritto nel browser web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` dell&#39;oggetto `getOutputContent` metodo.
   * Ottieni il tipo di contenuto del `com.adobe.idp.Document` oggetto richiamando il relativo `getContentType` metodo.
   * Imposta il `javax.servlet.http.HttpServletResponse` tipo di contenuto dell&#39;oggetto richiamando il relativo `setContentType` e passando il tipo di contenuto del `com.adobe.idp.Document` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser web client richiamando `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream` metodo.
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` dell&#39;oggetto `getInputStream` metodo.
   * Creare una matrice di byte e popolarla con il flusso di dati del modulo richiamando `InputStream` dell&#39;oggetto `read` e passando la matrice di byte come argomento.
   * Richiama `javax.servlet.ServletOutputStream` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

**Consulta anche**

[Rendering di Forms come HTML](#rendering-forms-as-html)

[Guida introduttiva (modalità SOAP): rendering di un modulo HTML tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eseguire il rendering di un modulo come HTML utilizzando l’API del servizio web {#render-a-form-as-html-using-the-web-service-api}

Eseguire il rendering di un modulo HTML utilizzando l’API Forms (servizio web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio Forms WSDL.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client di Forms

   Creare un `FormsService` e impostare i valori di autenticazione.

1. Imposta opzioni runtime di HTML

   * Creare un `HTMLRenderSpec` mediante il costruttore.
   * Per eseguire il rendering di un modulo HTML con una barra degli strumenti, richiamare `HTMLRenderSpec` dell&#39;oggetto `setHTMLToolbar` e passa un `HTMLToolbar` valore enum. Ad esempio, per visualizzare una barra degli strumenti HTML verticale, passare `HTMLToolbar.Vertical`.
   * Per impostare il valore locale per il modulo HTML, richiamare `HTMLRenderSpec` dell&#39;oggetto `setLocale` e passa un valore stringa che specifica il valore locale. Per ulteriori informazioni, consulta [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Per eseguire il rendering del modulo HTML all’interno di tag HTML completi, richiama `HTMLRenderSpec` dell&#39;oggetto `setOutputType` metodo e passaggio `OutputType.FullHTMLTags`.

   >[!NOTE]
   >
   Il rendering di Forms in HTML non viene eseguito correttamente quando `StandAlone` l&#39;opzione è `true` e `ApplicationWebRoot` fa riferimento a un server diverso dal server applicazioni J2EE che ospita AEM Forms (il `ApplicationWebRoot` il valore viene specificato utilizzando `URLSpec` oggetto passato al `FormsServiceClient` dell&#39;oggetto `(Deprecated) renderHTMLForm` metodo). Quando `ApplicationWebRoot` è un altro server di quello che ospita AEM Forms, il valore dell’URI della radice web nella console di amministrazione deve essere impostato come valore dell’URI dell’applicazione web del modulo. Per eseguire questa operazione, accedi alla console di amministrazione, fai clic su Servizi > Forms e imposta l’URI della directory principale del web come https://server-name:port/FormServer. Quindi, salva le impostazioni.

1. Rendering di un modulo HTML

   Richiama `FormsService` dell&#39;oggetto `(Deprecated) renderHTMLForm` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura di modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valore enum che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo di HTML compatibile con dynamic HTML per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * A `BLOB` oggetto contenente dati da unire con il modulo. Se non si desidera unire i dati, passare `null`. (vedere [Precompilazione di Forms con layout fluibili](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts).)
   * Il `HTMLRenderSpec` oggetto che memorizza le opzioni di runtime di HTML.
   * Un valore stringa che specifica il `HTTP_USER_AGENT` valore intestazione; ad esempio, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Se non si desidera impostare questo valore, è possibile passare una stringa vuota.
   * A `URLSpec` oggetto che memorizza i valori URI necessari per il rendering di un modulo HTML. (vedere [Specificare i valori URI](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * A `java.util.HashMap` oggetto che memorizza gli allegati. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera allegare file al modulo. (vedere [Allega file al modulo](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * Un campo vuoto `com.adobe.idp.services.holders.BLOBHolder` oggetto popolato dal metodo. Questo valore di parametro memorizza il modulo di cui è stato eseguito il rendering.
   * Un campo vuoto `com.adobe.idp.services.holders.BLOBHolder` oggetto popolato dal metodo. Questo parametro memorizza i dati XML di output.
   * Un campo vuoto `javax.xml.rpc.holders.LongHolder` oggetto popolato dal metodo. Questo argomento consente di memorizzare il numero di pagine nel modulo.
   * Un campo vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato dal metodo. Questo argomento consente di memorizzare il valore delle impostazioni locali.
   * Un campo vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato dal metodo. Questo argomento memorizza il valore di rendering HTML utilizzato.
   * Un campo vuoto `com.adobe.idp.services.holders.FormsResultHolder` oggetto che conterrà i risultati dell&#39;operazione.

   Il `(Deprecated) renderHTMLForm` il metodo compila `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come ultimo valore di argomento con un flusso di dati del modulo che deve essere scritto nel browser web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un `FormResult` dell&#39;oggetto ottenendo il valore del `com.adobe.idp.services.holders.FormsResultHolder` dell&#39;oggetto `value` membro dati.
   * Creare un `BLOB` oggetto che contiene i dati del modulo richiamando `FormsResult` dell&#39;oggetto `getOutputContent` metodo.
   * Ottieni il tipo di contenuto del `BLOB` oggetto richiamando il relativo `getContentType` metodo.
   * Imposta il `javax.servlet.http.HttpServletResponse` tipo di contenuto dell&#39;oggetto richiamando il relativo `setContentType` e passando il tipo di contenuto del `BLOB` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser web client richiamando `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream` metodo.
   * Creare una matrice di byte e popolarla richiamando il `BLOB` dell&#39;oggetto `getBinaryData` metodo. Questa attività assegna il contenuto del `FormsResult` alla matrice di byte.
   * Richiama `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

**Consulta anche**

[Rendering di Forms come HTML](#rendering-forms-as-html)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
