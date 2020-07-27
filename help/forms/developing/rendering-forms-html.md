---
title: Rendering dei moduli come HTML
seo-title: Rendering dei moduli come HTML
description: 'null'
seo-description: 'null'
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '4108'
ht-degree: 1%

---


# Rendering dei moduli come HTML {#rendering-forms-as-html}

Il servizio Forms esegue il rendering dei moduli come HTML in risposta a una richiesta HTTP inviata da un browser Web. Il rendering di un modulo in formato HTML può risultare vantaggioso se il computer in cui si trova il browser Web del client non richiede Adobe Reader, Acrobat o Flash Player (per le guide dei moduli (obsoleto)).

Per eseguire il rendering di un modulo come HTML, la struttura del modulo deve essere salvata come file XDP. Non è possibile eseguire il rendering HTML di una struttura del modulo salvata come file PDF. Durante lo sviluppo di una struttura del modulo in Designer che verrà rappresentata come HTML, tenere in considerazione i seguenti criteri:

* Non utilizzare le proprietà relative al bordo degli oggetti per disegnare righe, riquadri o griglie all’interno del modulo. In alcuni browser i bordi non vengono allineati esattamente come nell’anteprima di Gli oggetti possono risultare sovrapposti o impedire di visualizzare altri oggetti nella posizione prevista.
* Potete definire lo sfondo mediante linee, rettangoli e cerchi.
* Disegnate del testo leggermente più grande di quello che sembra necessario per contenere il testo. Alcuni browser Web non visualizzano il testo in modo leggibile.

>[!NOTE]
>
>Quando si esegue il rendering di un modulo che contiene immagini TIFF utilizzando i metodi `FormServiceClient` e `(Deprecated) renderHTMLForm` `renderHTMLForm2` dell&#39;oggetto, le immagini TIFF non sono visibili nel modulo HTML di cui è stato eseguito il rendering, visualizzato in Internet Explorer o nei browser Mozilla Firefox. Questi browser non forniscono supporto nativo per le immagini TIFF.

## Pagine HTML {#html-pages}

Durante il rendering di una struttura del modulo come modulo HTML, viene eseguito il rendering di ciascun sottomodulo di secondo livello come pagina HTML (pannello). È possibile visualizzare la gerarchia di un sottomodulo in Designer. I sottomoduli secondari appartenenti al sottomodulo principale (il nome predefinito di un sottomodulo principale è modulo1) sono i sottomoduli del pannello. L&#39;esempio seguente mostra i sottomoduli di una struttura del modulo.

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

Durante il rendering delle strutture del modulo come moduli HTML, i pannelli non sono vincolati a particolari dimensioni di pagina. Se si dispone di sottomoduli dinamici, questi dovrebbero essere nidificati all&#39;interno del sottomodulo del pannello. I sottomoduli dinamici sono in grado di espandersi fino a un numero infinito di pagine HTML.

Quando si esegue il rendering di un modulo HTML, le dimensioni di pagina (necessarie per l&#39;impaginazione dei moduli rappresentati in PDF) non hanno alcun significato. Poiché un modulo con layout scorrevole può espandersi fino a un numero infinito di pagine HTML, è importante evitare che sulla pagina master siano presenti dei piè di pagina. Un piè di pagina sotto l&#39;area contenuto di una pagina master può sovrascrivere il contenuto HTML che scorre oltre il limite di una pagina.

È necessario passare esplicitamente da un pannello all’altro utilizzando i metodi `xfa.host.pageUp` e `xfa.host.pageDown` . Per modificare le pagine, è necessario inviare un modulo al servizio Forms e fare in modo che il servizio Forms esegua il rendering del modulo sul dispositivo client, in genere un browser Web.

>[!NOTE]
>
>Il processo di invio di un modulo al servizio Forms e successivo rendering del modulo da parte del servizio Forms sul dispositivo client è definito come ciclo di dati per il passaggio al server.

>[!NOTE]
>
>Se si desidera personalizzare l&#39;aspetto del pulsante Firma digitale HTML in un modulo HTML, è necessario modificare le seguenti proprietà nel file fscdigsig.css (all&#39;interno del file adobe-forms-ds.ear > adobe-forms-ds.war):

**.fsc-ds-ssb**: Questo foglio di stile è applicabile nel caso di un campo di firma vuoto.

**.fsc-ds-ssv**: Questo foglio di stile è applicabile nel caso di un campo di firma valido.

**.fsc-ds-ssc**: Questo foglio di stile è applicabile nel caso di un campo di firma valido ma i dati sono cambiati.

**.fsc-ds-ssi**: Questo foglio di stile è applicabile nel caso di un campo di firma non valido.

**.fsc-ds-popup-bg**: Questa proprietà del foglio di stile non viene utilizzata.

**.fsc-ds-popup-btn**: Questa proprietà del foglio di stile non viene utilizzata.

## Esecuzione di script {#running-scripts}

L&#39;autore di un modulo specifica se uno script viene eseguito sul server o sul client. Il servizio Forms crea un ambiente di elaborazione eventi distribuito per l&#39;esecuzione di informazioni sui moduli che possono essere distribuite tra il client e il server utilizzando l&#39; `runAt` attributo . Per informazioni su questo attributo o sulla creazione di script all&#39;interno delle strutture del modulo, vedere [Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Il servizio Forms è in grado di eseguire gli script durante il rendering del modulo. Di conseguenza, è possibile precompilare un modulo con i dati connettendosi a un database o a servizi Web che potrebbero non essere disponibili sul client. Potete anche impostare l&#39; `Click` evento di un pulsante da eseguire sul server in modo che il client esegua il ciclo dei dati sul server. Questo consente al client di eseguire script che possono richiedere risorse server, ad esempio un database aziendale, mentre l&#39;utente interagisce con un modulo. Per i moduli HTML, gli script di formcalc possono essere eseguiti solo sul server. Di conseguenza, è necessario contrassegnare questi script per l&#39;esecuzione in `server` o `both`.

È possibile progettare moduli che si spostano tra le pagine (pannelli) chiamando `xfa.host.pageUp` e `xfa.host.pageDown` utilizzando metodi. Questo script viene posizionato nell&#39; `Click` &#39;evento di un pulsante e l&#39; `runAt` attributo è impostato su `Both`. È quindi `Both` possibile scegliere Adobe Reader o Acrobat (per i moduli di cui viene eseguito il rendering in formato PDF) per modificare le pagine senza passare al server e i moduli HTML possono modificare le pagine arrotondando i dati al server. In altre parole, un modulo viene inviato al servizio Forms e viene riprodotto come HTML con la nuova pagina visualizzata.

Si consiglia di non assegnare alle variabili di script e ai campi modulo gli stessi nomi, ad esempio item. Alcuni browser Web, come Internet Explorer, potrebbero non inizializzare una variabile con lo stesso nome di un campo di modulo che genera un errore di script. È buona norma assegnare ai campi del modulo e alle variabili di script nomi diversi.

Quando si esegue il rendering di moduli HTML contenenti sia la funzionalità di navigazione delle pagine che gli script di un modulo (ad esempio, se uno script recupera dati di campo da un database ogni volta che viene eseguito il rendering del modulo), assicurarsi che lo script del modulo si trovi nell&#39;evento form:calculate anziché nell&#39;evento form:readyevent.

Gli script del modulo che si trovano nell&#39;evento form:ready vengono eseguiti solo una volta durante il rendering iniziale del modulo e non vengono eseguiti per recuperi successivi della pagina. Al contrario, l&#39;evento form:calculate viene eseguito per ogni spostamento di pagina in cui viene eseguito il rendering del modulo.

>[!NOTE]
In un modulo con più pagine, le modifiche apportate da JavaScript a una pagina non vengono mantenute se si passa a un&#39;altra pagina.

È possibile richiamare script personalizzati prima di inviare il modulo. Questa funzione funziona su tutti i browser disponibili. Tuttavia, può essere utilizzato solo quando gli utenti eseguono il rendering del modulo HTML con la `Output Type` proprietà impostata su `Form Body`. Non funzionerà quando `Output Type` è `Full HTML`. Per i passaggi necessari per configurare questa funzione, fare riferimento alla sezione Configurazione dei moduli nella guida di amministrazione.

È innanzitutto necessario definire una funzione di callback chiamata prima di inviare il modulo, dove si trova il nome della funzione `_user_onsubmit`. Si presume che la funzione non genererà alcuna eccezione, o in caso contrario, che l&#39;eccezione venga ignorata. Si consiglia di inserire la funzione JavaScript nella sezione head del html; tuttavia, è possibile dichiararlo ovunque prima della fine dei tag script che includono `xfasubset.js`.

Quando formserver esegue il rendering di un XDP contenente un elenco a discesa, oltre alla creazione dell&#39;elenco a discesa, crea anche due campi di testo nascosti. Questi campi di testo memorizzano i dati dell&#39;elenco a discesa (uno memorizza il nome visualizzato delle opzioni e l&#39;altro memorizza il valore per le opzioni). Pertanto, ogni volta che un utente invia il modulo, vengono inviati tutti i dati dell&#39;elenco a discesa. Presupponendo che non si desideri inviare la maggior parte dei dati ogni volta, è possibile scrivere uno script personalizzato per disattivarlo. Ad esempio: Il nome dell&#39;elenco a discesa è racchiuso `drpOrderedByStateProv` nell&#39;intestazione del sottomodulo. Il nome dell&#39;elemento di input HTML sarà `header[0].drpOrderedByStateProv[0]`. Il nome dei campi nascosti che archiviano e inviano i dati del menu a discesa ha i seguenti nomi: `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

Se non si desidera inviare i dati, è possibile disattivare questi elementi di input nel modo seguente. `var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

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

Quando si creano strutture del modulo per il rendering come HTML, è necessario limitare lo script al sottoinsieme XFA per gli script nel linguaggio JavaScript.

Gli script eseguiti sul client o eseguiti sia sul client che sul server devono essere scritti all&#39;interno del sottoinsieme XFA. Gli script eseguiti sul server possono utilizzare il modello di script XFA completo e FormCalc. Per informazioni sull&#39;uso di JavaScript, vedere [Designer](https://www.adobe.com/go/learn_aemforms_designer_63)di moduli.

Quando si eseguono script sul client, è possibile utilizzare script solo il pannello corrente visualizzato; ad esempio, non è possibile eseguire script rispetto ai campi che si trovano nel pannello A quando viene visualizzato il pannello B. Durante l&#39;esecuzione degli script sul server, è possibile accedere a tutti i pannelli.

È inoltre necessario prestare attenzione quando si utilizzano espressioni SOM (Scripting Object Model) all&#39;interno di script eseguiti sul client. Solo un sottoinsieme semplificato di espressioni SOM è supportato da script eseguiti sul client.

## Tempistica evento {#event-timing}

Il sottoinsieme XFA definisce gli eventi XFA mappati a eventi HTML. Esiste una leggera differenza di comportamento nella tempistica degli eventi calculate e validate. In un browser Web, viene eseguito un evento calculate completo quando si esce da un campo. Gli eventi di calcolo non vengono eseguiti automaticamente quando si apporta una modifica al valore di un campo. È possibile forzare un evento calculate chiamando il `xfa.form.execCalculate` metodo.

In un browser Web, gli eventi validate vengono eseguiti solo all&#39;uscita da un campo o all&#39;invio di un modulo. È possibile forzare un evento validate utilizzando il `xfa.form.execValidate` metodo .

I moduli visualizzati in un browser Web (a differenza di Adobe Reader o Acrobat) sono conformi al test null (errori o avvisi) XFA per i campi obbligatori.

* Se il test null genera un errore e si esce da un campo senza specificare un valore, dopo aver fatto clic su OK viene visualizzata una finestra di messaggio che consente di riposizionare il campo.
* Se un test null genera un avviso e si esce da un campo senza specificare un valore, viene richiesto di fare clic su OK o Annulla, consentendo di procedere senza specificare un valore o di tornare al campo per immettere un valore.

Per ulteriori informazioni su un test null, vedere [Designer](https://www.adobe.com/go/learn_aemforms_designer_63)di moduli.

## Pulsanti Modulo {#form-buttons}

Facendo clic su un pulsante di invio, i dati del modulo vengono inviati al servizio Forms e rappresenta la fine dell&#39;elaborazione del modulo. L&#39; `preSubmit` evento può essere impostato per essere eseguito sul client o sul server. L&#39; `preSubmit` evento viene eseguito prima dell&#39;invio del modulo, se configurato per essere eseguito sul client. In caso contrario, l&#39; `preSubmit` evento viene eseguito sul server durante l&#39;invio del modulo. Per ulteriori informazioni sull&#39; `preSubmit` evento, vedere [Designer](https://www.adobe.com/go/learn_aemforms_designer_63)di moduli.

Se a un pulsante non è associato alcuno script sul lato client, i dati vengono inviati al server, i calcoli vengono eseguiti sul server e il modulo HTML viene rigenerato. Se un pulsante contiene uno script sul lato client, i dati non vengono inviati al server e lo script sul lato client viene eseguito nel browser Web.

## Browser Web HTML 4.0 {#html-4-0-web-browser}

Un browser Web che supporta solo HTML 4.0 non può supportare il modello di script lato client del sottoinsieme XFA. Durante la creazione di una struttura del modulo da utilizzare sia in HTML 4.0 che in MSDHTML o CSS2HTML, uno script contrassegnato per l&#39;esecuzione sul client verrà eseguito sul server. Ad esempio, si supponga che l&#39;utente faccia clic su un pulsante situato in un modulo visualizzato in un browser Web HTML 4.0. In questa situazione, i dati del modulo vengono inviati al server in cui viene eseguito lo script sul lato client.

È consigliabile inserire la logica del modulo negli eventi calculate, che vengono eseguiti sul server in HTML 4.0 e sul client per MSDHTML o CSS2HTML.

## Gestione delle modifiche alla presentazione {#maintaining-presentation-changes}

Quando vi spostate tra le pagine HTML (pannelli), viene mantenuto solo lo stato dei dati. Le impostazioni come il colore di sfondo o le impostazioni obbligatorie del campo non vengono mantenute (se diverse dalle impostazioni iniziali). Per mantenere lo stato della presentazione, dovete creare dei campi (solitamente nascosti) che rappresentano lo stato della presentazione dei campi. Se aggiungete uno script all&#39; `Calculate` evento di un campo che modifica la presentazione in base ai valori dei campi nascosti, potete mantenere lo stato della presentazione mentre vi spostate avanti e indietro tra le pagine HTML (pannelli).

Lo script seguente mantiene l&#39;aspetto `fillColor` di un campo in base al valore di `hiddenField`. Si supponga che questo script si trovi nell&#39; `Calculate` evento del campo.

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
Gli oggetti statici non vengono visualizzati in un modulo HTML di cui è stato eseguito il rendering quando nidificati all&#39;interno di una cella di tabella. Ad esempio, un cerchio e un rettangolo nidificati all&#39;interno di una cella di tabella non vengono visualizzati all&#39;interno di un modulo HTML di rendering. Tuttavia, questi stessi oggetti statici vengono visualizzati correttamente quando si trovano all&#39;esterno della tabella.

## Firma digitale di moduli HTML {#digitally-signing-html-forms}

Non è possibile firmare un modulo HTML che contiene un campo firma digitale se il modulo viene rappresentato come una delle seguenti trasformazioni HTML:

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

Per informazioni sulla firma digitale di un documento, vedere Firma [digitale e certificazione dei documenti](/help/forms/developing/digitally-signing-certifying-documents.md)

## Rendering di un modulo XHTML conforme alle linee guida per l&#39;accesso facilitato {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

È possibile eseguire il rendering di un modulo HTML completo conforme alle linee guida per l&#39;accessibilità. In altre parole, il rendering del modulo viene eseguito all&#39;interno di tag HTML completi, al contrario del rendering del modulo HTML all&#39;interno dei tag body (non una pagina HTML completa).

## Convalida dei dati del modulo {#validating-form-data}

È consigliabile limitare l&#39;uso delle regole di convalida per i campi modulo durante il rendering del modulo come modulo HTML. Alcune regole di convalida potrebbero non essere supportate per i moduli HTML. Ad esempio, quando un pattern di convalida MM-GG-AAAA viene applicato a un `Date/Time` campo che si trova in una struttura del modulo rappresentata come modulo HTML, non funziona correttamente, anche se la data viene digitata correttamente. Tuttavia, questo pattern di convalida funziona correttamente per i moduli sottoposti a rendering come PDF.

>[!NOTE]
Per ulteriori informazioni sul servizio Forms, vedere Riferimento [servizi per gli AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo HTML, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto API client Forms.
1. Impostare le opzioni di runtime HTML.
1. Eseguire il rendering di un modulo HTML.
1. Scrivere il flusso di dati del modulo nel browser Web del client.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Forms**

Prima di poter importare i dati in un&#39;API formClient PDF a livello di programmazione, è necessario creare un client del servizio di integrazione dati modulo. Quando create un client di servizi, definite le impostazioni di connessione necessarie per richiamare un servizio.

**Impostazione delle opzioni di runtime HTML**

È possibile impostare le opzioni di runtime HTML al momento del rendering di un modulo HTML. Ad esempio, è possibile aggiungere una barra degli strumenti a un modulo HTML per consentire agli utenti di selezionare i file allegati che si trovano sul computer client o di recuperare i file allegati di cui viene eseguito il rendering con il modulo HTML. Per impostazione predefinita, una barra degli strumenti HTML è disabilitata. Per aggiungere una barra degli strumenti a un modulo HTML, è necessario impostare in modo programmatico le opzioni di esecuzione. Per impostazione predefinita, una barra degli strumenti HTML è composta dai seguenti pulsanti:

* `Home`: Fornisce un collegamento alla directory principale Web dell&#39;applicazione.
* `Upload`: Fornisce un&#39;interfaccia utente per selezionare i file da allegare al modulo corrente.
* `Download`: Fornisce un&#39;interfaccia utente per visualizzare i file allegati.

Quando in un modulo HTML viene visualizzata una barra degli strumenti HTML, l&#39;utente può selezionare un massimo di dieci file da inviare insieme ai dati del modulo. Una volta inviati i file, il servizio Forms è in grado di recuperarli.

Quando si esegue il rendering di un modulo come HTML, è possibile specificare un valore agente utente. Un valore agente utente fornisce informazioni su browser e sistema. Si tratta di un valore facoltativo e potete trasmettere un valore di stringa vuoto. Il rendering di un modulo HTML tramite l&#39;avvio rapido di Java API mostra come ottenere un valore agente utente e utilizzarlo per eseguire il rendering di un modulo come HTML.

Gli URL HTTP a cui vengono inviati i dati del modulo possono essere specificati impostando l&#39;URL di destinazione mediante l&#39;API client di Forms Service oppure specificati nel pulsante Invia contenuto nella struttura del modulo XDP. Se l&#39;URL di destinazione è specificato nella struttura del modulo, non impostare un valore utilizzando l&#39;API client di Forms Service.

>[!NOTE]
Il rendering di un modulo HTML con una barra degli strumenti è facoltativo.

>[!NOTE]
Se si esegue il rendering di un modulo AHTML, si consiglia di non aggiungere al modulo una barra degli strumenti.

**Eseguire il rendering di un modulo HTML**

Per eseguire il rendering di un modulo HTML, è necessario specificare una struttura del modulo creata in Designer e salvata come file XDP. È inoltre necessario selezionare un tipo di trasformazione HTML. Ad esempio, potete specificare il tipo di trasformazione HTML che esegue il rendering di un HTML dinamico per Internet Explorer 5.0 o versione successiva.

Il rendering di un modulo HTML richiede anche valori, ad esempio valori URI, necessari per eseguire il rendering di altri tipi di modulo.

**Scrivere il flusso di dati del modulo nel browser Web del client**

Quando il servizio Forms esegue il rendering di un modulo HTML, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web del client. Una volta scritto nel browser Web del client, il modulo HTML è visibile all&#39;utente.

**Consulta anche**

[Eseguire il rendering di un modulo come HTML utilizzando l&#39;API Java](#render-a-form-as-html-using-the-java-api)

[Eseguire il rendering di un modulo come HTML utilizzando l&#39;API del servizio Web](#render-a-form-as-html-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendering di moduli HTML con barre degli strumenti personalizzate](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[Creazione di applicazioni Web per il rendering di moduli](/help/forms/developing/creating-web-applications-renders-forms.md)

## Eseguire il rendering di un modulo come HTML utilizzando l&#39;API Java {#render-a-form-as-html-using-the-java-api}

Eseguire il rendering di un modulo HTML utilizzando l&#39;API Forms (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Forms

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `FormsServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Impostazione delle opzioni di runtime HTML

   * Creare un `HTMLRenderSpec` oggetto utilizzando il relativo costruttore.
   * Per eseguire il rendering di un modulo HTML con una barra degli strumenti, richiamare il metodo dell&#39; `HTMLRenderSpec` oggetto `setHTMLToolbar` e passare un valore `HTMLToolbar` enum. Ad esempio, per visualizzare una barra degli strumenti HTML verticale, passare `HTMLToolbar.Vertical`.
   * Per impostare il valore delle impostazioni internazionali per il modulo HTML, richiamare il metodo dell&#39; `HTMLRenderSpec` oggetto `setLocale` e passare una stringa che specifica il valore delle impostazioni internazionali. (Questa è un&#39;impostazione opzionale).
   * Per eseguire il rendering del modulo HTML all&#39;interno di tag HTML completi, richiamare il metodo dell&#39; `HTMLRenderSpec` oggetto `setOutputType` e passare `OutputType.FullHTMLTags`. (Questa è un&#39;impostazione opzionale).

   >[!NOTE]
   Il rendering dei moduli non viene eseguito correttamente in HTML quando l&#39; `StandAlone` opzione è `true` e `ApplicationWebRoot` fa riferimento a un server diverso dai AEM Forms del server applicazione J2EE (il `ApplicationWebRoot` valore viene specificato utilizzando l&#39; `URLSpec` oggetto passato al `FormsServiceClient` metodo dell&#39; `(Deprecated) renderHTMLForm` oggetto). Se `ApplicationWebRoot` si tratta di un altro server appartenente a uno dei AEM Forms host, il valore dell&#39;URI della radice Web nella console di amministrazione deve essere impostato come valore URI dell&#39;applicazione Web Form. A tale scopo, accedere alla console di amministrazione, fare clic su Servizi > Moduli e impostare l&#39;URI della directory principale Web come https://server-name:port/FormServer. Quindi, salvate le impostazioni.

1. Eseguire il rendering di un modulo HTML

   Richiama il metodo dell’ `FormsServiceClient` oggetto `(Deprecated) renderHTMLForm` e passa i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valore `TransformTo` enum che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con HTML dinamico per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * Un `com.adobe.idp.Document` oggetto che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare un `com.adobe.idp.Document` oggetto vuoto.
   * L&#39; `HTMLRenderSpec` oggetto che memorizza le opzioni di runtime HTML.
   * Un valore di stringa che specifica il valore dell&#39; `HTTP_USER_AGENT` intestazione; ad esempio, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Un `URLSpec` oggetto che memorizza i valori URI richiesti per eseguire il rendering di un modulo HTML.
   * Un `java.util.HashMap` oggetto che memorizza gli allegati. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate allegare file al modulo.

   Il `(Deprecated) renderHTMLForm` metodo restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo che può essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` metodo ‘s `getOutputContent` .
   * Ottenere il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto richiamandone il `getContentType` metodo.
   * Impostare il tipo di contenuto dell&#39; `javax.servlet.http.HttpServletResponse` oggetto richiamandone `setContentType` il metodo e passando il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il `javax.servlet.http.HttpServletResponse` metodo dell&#39; `getOutputStream` oggetto.
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` metodo dell&#39; `getInputStream` oggetto.
   * Creare un array di byte e compilarlo con il flusso di dati del modulo richiamando il metodo dell&#39; `InputStream` oggetto `read` e passando l&#39;array di byte come argomento.
   * Richiamare il metodo dell&#39; `javax.servlet.ServletOutputStream` oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passa l&#39;array di byte al `write` metodo.

**Consulta anche**

[Rendering dei moduli come HTML](#rendering-forms-as-html)

[Avvio rapido (modalità SOAP): Rendering di un modulo HTML utilizzando l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eseguire il rendering di un modulo come HTML utilizzando l&#39;API del servizio Web {#render-a-form-as-html-using-the-web-service-api}

Eseguire il rendering di un modulo HTML utilizzando l&#39;API Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il WSDL del servizio Forms.
   * Includete le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client Forms

   Creare un `FormsService` oggetto e impostare i valori di autenticazione.

1. Impostazione delle opzioni di runtime HTML

   * Creare un `HTMLRenderSpec` oggetto utilizzando il relativo costruttore.
   * Per eseguire il rendering di un modulo HTML con una barra degli strumenti, richiamare il metodo dell&#39; `HTMLRenderSpec` oggetto `setHTMLToolbar` e passare un valore `HTMLToolbar` enum. Ad esempio, per visualizzare una barra degli strumenti HTML verticale, passare `HTMLToolbar.Vertical`.
   * Per impostare il valore delle impostazioni internazionali per il modulo HTML, richiamare il metodo dell&#39; `HTMLRenderSpec` oggetto `setLocale` e passare una stringa che specifica il valore delle impostazioni internazionali. Per ulteriori informazioni, consulta [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)(Riferimento API per gli ).
   * Per eseguire il rendering del modulo HTML all&#39;interno di tag HTML completi, richiamare il metodo dell&#39; `HTMLRenderSpec` oggetto `setOutputType` e passare `OutputType.FullHTMLTags`.

   >[!NOTE]
   Il rendering dei moduli non viene eseguito correttamente in HTML quando l&#39; `StandAlone` opzione è `true` e `ApplicationWebRoot` fa riferimento a un server diverso dai AEM Forms del server applicazione J2EE (il `ApplicationWebRoot` valore viene specificato utilizzando l&#39; `URLSpec` oggetto passato al `FormsServiceClient` metodo dell&#39; `(Deprecated) renderHTMLForm` oggetto). Se `ApplicationWebRoot` si tratta di un altro server appartenente a uno dei AEM Forms host, il valore dell&#39;URI della radice Web nella console di amministrazione deve essere impostato come valore URI dell&#39;applicazione Web Form. A tale scopo, accedere alla console di amministrazione, fare clic su Servizi > Moduli e impostare l&#39;URI della directory principale Web come https://server-name:port/FormServer. Quindi, salvate le impostazioni.

1. Eseguire il rendering di un modulo HTML

   Richiama il metodo dell’ `FormsService` oggetto `(Deprecated) renderHTMLForm` e passa i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valore `TransformTo` enum che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con HTML dinamico per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * Un `BLOB` oggetto che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare `null`. (Vedere [Precompilazione dei moduli con layout](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts)scorrevoli.)
   * L&#39; `HTMLRenderSpec` oggetto che memorizza le opzioni di runtime HTML.
   * Un valore di stringa che specifica il valore dell&#39; `HTTP_USER_AGENT` intestazione; ad esempio, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Se non si desidera impostare questo valore, è possibile passare una stringa vuota.
   * Un `URLSpec` oggetto che memorizza i valori URI richiesti per eseguire il rendering di un modulo HTML. Consultate [Specificare i valori](/help/forms/developing/rendering-interactive-pdf-forms.md)URI.
   * Un `java.util.HashMap` oggetto che memorizza gli allegati. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate allegare file al modulo. (Vedere [Allegare file al modulo](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * Un oggetto vuoto `com.adobe.idp.services.holders.BLOBHolder` compilato dal metodo. Questo valore del parametro memorizza il modulo di cui è stato effettuato il rendering.
   * Un oggetto vuoto `com.adobe.idp.services.holders.BLOBHolder` compilato dal metodo. Questo parametro memorizzerà i dati XML di output.
   * Un oggetto vuoto `javax.xml.rpc.holders.LongHolder` compilato dal metodo. Questo argomento consente di memorizzare il numero di pagine nel modulo.
   * Un oggetto vuoto `javax.xml.rpc.holders.StringHolder` compilato dal metodo. Questo argomento memorizzerà il valore delle impostazioni internazionali.
   * Un oggetto vuoto `javax.xml.rpc.holders.StringHolder` compilato dal metodo. Questo argomento memorizzerà il valore di rendering HTML utilizzato.
   * Un oggetto vuoto `com.adobe.idp.services.holders.FormsResultHolder` che conterrà i risultati dell&#39;operazione.

   Il `(Deprecated) renderHTMLForm` metodo compila l&#39; `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come valore dell&#39;ultimo argomento con un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un `FormResult` oggetto ottenendo il valore del membro `com.adobe.idp.services.holders.FormsResultHolder` dati dell&#39; `value` oggetto.
   * Creare un `BLOB` oggetto che contenga dati del modulo richiamando il `FormsResult` metodo dell&#39; `getOutputContent` oggetto.
   * Ottenere il tipo di contenuto dell&#39; `BLOB` oggetto richiamandone il `getContentType` metodo.
   * Impostare il tipo di contenuto dell&#39; `javax.servlet.http.HttpServletResponse` oggetto richiamandone `setContentType` il metodo e passando il tipo di contenuto dell&#39; `BLOB` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il `javax.servlet.http.HttpServletResponse` metodo dell&#39; `getOutputStream` oggetto.
   * Creare un array di byte e compilarlo richiamando il metodo dell&#39; `BLOB` oggetto `getBinaryData` . Questa attività assegna il contenuto dell&#39; `FormsResult` oggetto all&#39;array di byte.
   * Richiamare il metodo dell&#39; `javax.servlet.http.HttpServletResponse` oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passa l&#39;array di byte al `write` metodo.

**Consulta anche**

[Rendering dei moduli come HTML](#rendering-forms-as-html)

[Chiamata di AEM Forms mediante codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

