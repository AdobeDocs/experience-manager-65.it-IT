---
title: Incorporare un modulo adattivo in una pagina web esterna
seo-title: Incorporare un modulo adattivo in una pagina web esterna
description: Scopri come incorporare un modulo adattivo in una pagina web esterna
seo-description: Scopri come incorporare un modulo adattivo in una pagina web HTML esterna
uuid: d81032dd-af80-4f4b-a717-ee1b89fd3d3d
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: author
discoiquuid: d739c6da-3b41-4452-8728-d7cd1a3ae20b
docset: aem65
feature: Moduli adattivi
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 2%

---


# Incorporare un modulo adattivo in una pagina web esterna{#embed-adaptive-form-in-external-web-page}

È possibile [incorporare moduli adattivi in una pagina AEM Sites](/help/forms/using/embed-adaptive-form-aem-sites.md) o in una pagina web ospitata all&#39;esterno di AEM. Il modulo adattivo incorporato è completamente funzionale e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente all’utente di rimanere nel contesto di altri elementi della pagina web e di interagire contemporaneamente con il modulo.

## Prerequisiti {#prerequisites}

Esegui i seguenti passaggi prima di incorporare un modulo adattivo in un sito Web esterno

* Pubblica il modulo adattivo da incorporare nell’istanza di pubblicazione del server AEM Forms.
* Crea o identifica una pagina web sul tuo sito web per ospitare il modulo adattivo. Assicurati che la pagina web possa [leggere i file jQuery da una CDN](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js) o che abbia una copia locale della jQuery incorporata. jQuery è necessario per eseguire il rendering di un modulo adattivo.
* Quando AEM server e la pagina web si trovano su domini diversi, esegui i passaggi elencati nella sezione [consenti ad AEM Forms di distribuire moduli adattivi a un sito con più domini](#cross-site).

## Incorpora modulo adattivo {#embed-adaptive-form}

È possibile incorporare un modulo adattivo inserendo alcune righe di JavaScript nella pagina web. L’API nel codice invia una richiesta HTTP al server AEM per le risorse dei moduli adattivi e inserisce il modulo adattivo nel contenitore di moduli specificato.

Per incorporare il modulo adattivo:

1. Crea una pagina web sul tuo sito web con il seguente codice:

   ```html
   <!doctype html>
   <html>
     <head>
       <title>This is the title of the webpage!</title>
       <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
     </head>
     <body>
     <div class="customafsection"/>
       <p>This section is replaced with the adaptive form.</p>
   
    <script>
    var options = {path:"/content/forms/af/locbasic.html", dataRef:"", themepath:"", CSS_Selector:".customafsection"};
    alert(options.path);
    var loadAdaptiveForm = function(options){
    //alert(options.path);
       if(options.path) {
           // options.path refers to the publish URL of the adaptive form
           // For Example: https:myserver:4503/content/forms/af/ABC, where ABC is the adaptive form
           // Note: If AEM server is running on a context path, the adaptive form URL must contain the context path
           var path = options.path;
           path += "/jcr:content/guideContainer.html";
           $.ajax({
               url  : path ,
               type : "GET",
               data : {
                   // Set the wcmmode to be disabled
                   wcmmode : "disabled"
                   // Set the data reference, if any
                  // "dataRef": options.dataRef
                   // Specify a different theme for the form object
                 //  "themeOverride" : options.themepath
               },
               async: false,
               success: function (data) {
                   // If jquery is loaded, set the inner html of the container
                   // If jquery is not loaded, use APIs provided by document to set the inner HTML but these APIs would not evaluate the script tag in HTML as per the HTML5 spec
                   // For example: document.getElementById().innerHTML
                   if(window.$ && options.CSS_Selector){
                       // HTML API of jquery extracts the tags, updates the DOM, and evaluates the code embedded in the script tag.
                       $(options.CSS_Selector).html(data);
                   }
               },
               error: function (data) {
                   // any error handler
               }
           });
       } else {
           if (typeof(console) !== "undefined") {
               console.log("Path of Adaptive Form not specified to loadAdaptiveForm");
           }
       }
    }(options);
   
    </script>
     </body>
   </html>
   ```

1. Nel codice incorporato:

   * Modifica il valore della variabile *options.path* con il percorso dell&#39;URL di pubblicazione del modulo adattivo. Se il server AEM è in esecuzione su un percorso contestuale, assicurati che l’URL includa il percorso contestuale. menziona sempre il nome completo del modulo adattivo, inclusa l’estensione.   Ad esempio, il codice e l’adattivo di cui sopra risiedono sullo stesso server di moduli AEM in modo che l’esempio utilizzi il percorso contestuale del modulo adattivo /content/forms/af/locbasic.html.
   * Sostituisci *options.dataRef* con gli attributi da passare con l&#39;URL. Puoi usare la variabile dataref per [precompilare un modulo adattivo](/help/forms/using/prepopulate-adaptive-form-fields.md).
   * Sostituisci *options.themePath* con il percorso di un tema diverso da quello configurato nel modulo adattivo. In alternativa, puoi specificare il percorso del tema utilizzando l’attributo di richiesta.
   * CSS_Selector è il selettore CSS del contenitore di moduli in cui è incorporato il modulo adattivo. Ad esempio, la classe css .customafsection è il selettore CSS nell&#39;esempio precedente.

Il modulo adattivo è incorporato nella pagina web. Osserva quanto segue nel modulo adattivo incorporato:

* Le intestazioni e i piè di pagina nel modulo adattivo originale non sono inclusi nel modulo incorporato.
* Le bozze e i moduli inviati sono disponibili nella scheda Bozze e invii del portale Forms.
* L’azione di invio configurata sul modulo adattivo originale viene mantenuta nel modulo incorporato.
* Le regole del modulo adattivo vengono mantenute e completamente funzionanti nel modulo incorporato.
* Il targeting delle esperienze e i test A/B configurati nel modulo adattivo originale non funzionano nel modulo incorporato.
* Se Adobe Analytics è configurato sul modulo originale, i dati di analisi vengono acquisiti nel server Adobe Analytics. Tuttavia, non è disponibile nel rapporto di Forms Analytics.

## Topologia di esempio {#sample-topology}

La pagina web esterna che incorpora il modulo adattivo invia richieste al server AEM, che in genere si trova dietro il firewall in una rete privata. Per garantire che le richieste siano indirizzate in modo sicuro al server AEM, si consiglia di impostare un server reverse proxy.

Diamo un esempio di come impostare un server proxy inverso Apache 2.4 senza dispatcher. In questo esempio, ospiterai il server AEM con il percorso contestuale `/forms` e mapperai `/forms` per il proxy inverso. In questo modo, qualsiasi richiesta per `/forms` sul server Apache viene indirizzata all&#39;istanza AEM. Questa topologia consente di ridurre il numero di regole a livello del dispatcher, in quanto tutte le richieste hanno il prefisso `/forms` indirizzamento al server AEM.

1. Apri il file di configurazione `httpd.conf` e rimuovi il commento dalle seguenti righe di codice. In alternativa, è possibile aggiungere queste righe di codice nel file .

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. Imposta le regole proxy aggiungendo le seguenti righe di codice nel file di configurazione `httpd-proxy.conf` .

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   Sostituisci `[AEM_Instance]` con l&#39;URL di pubblicazione del server AEM nelle regole.

Se non installi il server AEM su un percorso contestuale, le regole proxy su Apache layer saranno le seguenti:

```text
ProxyPass /content https://<AEM_Instance>/content
ProxyPass /etc https://<AEM_Instance>/etc
ProxyPass /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# CSRF Filter
ProxyPass /libs/granite/csrf/token.json https://<AEM_Instance>/libs/granite/csrf/token.json

ProxyPassReverse /etc https://<AEM_Instance>/etc
ProxyPassReverse /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# written for thank you page and other URL present in AF during redirect
ProxyPassReverse /content https://<AEM_Instance>/content
```

>[!NOTE]
>
>Se imposti un’altra topologia, accertati di aggiungere gli URL di invio, precompilazione e altri URL all’inserire nell&#39;elenco Consentiti del livello del dispatcher.

## Best practice {#best-practices}

Quando incorpori un modulo adattivo in una pagina web, considera le seguenti best practice:

* Assicurati che le regole di stile definite nel CSS della pagina web non siano in conflitto con il CSS dell’oggetto modulo. Per evitare i conflitti, puoi riutilizzare il CSS della pagina web nel tema del modulo adattivo utilizzando AEM libreria client. Per informazioni sull&#39;utilizzo della libreria client nei temi dei moduli adattivi, consulta [Temi in AEM Forms](../../forms/using/themes.md).
* Fare in modo che il contenitore del modulo nella pagina Web utilizzi l’intera larghezza della finestra. Garantisce che le regole CSS configurate per i dispositivi mobili funzionino senza alcuna modifica. Se il contenitore modulo non ha l’intera larghezza della finestra, è necessario scrivere CSS personalizzati per adattare il modulo a diversi dispositivi mobili.
* Utilizza l’API `[getData](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` per ottenere la rappresentazione XML o JSON dei dati del modulo nel client.
* Utilizza `[unloadAdaptiveForm](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API per scaricare il modulo adattivo dal DOM HTML.
* Imposta l&#39;intestazione access-control-origin durante l&#39;invio della risposta da AEM server.

## Abilitare AEM Forms a distribuire moduli adattivi a un sito tra più domini {#cross-site}

1. In AEM&#39;istanza di pubblicazione, vai a AEM Web Console Configuration Manager all&#39;indirizzo `https://'[server]:[port]'/system/console/configMgr`.
1. Individua e apri la configurazione **Apache Sling Referrer Filter** .
1. Nel campo Host consentiti , specifica il dominio in cui si trova la pagina web. Consente all’host di effettuare richieste POST al server AEM. Puoi inoltre utilizzare l’espressione regolare per specificare una serie di domini di applicazione esterni.
