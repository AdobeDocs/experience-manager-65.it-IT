---
title: Incorpora modulo adattivo in una pagina Web esterna
seo-title: Incorpora modulo adattivo in una pagina Web esterna
description: Informazioni su come incorporare un modulo adattivo in una pagina Web esterna
seo-description: Informazioni su come incorporare un modulo adattivo in una pagina Web HTML esterna
uuid: d81032dd-af80-4f4b-a717-ee1b89fd3d3d
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: author
discoiquuid: d739c6da-3b41-4452-8728-d7cd1a3ae20b
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 0%

---


# Incorpora modulo adattivo in una pagina Web esterna{#embed-adaptive-form-in-external-web-page}

È possibile [incorporare moduli adattivi in una pagina](/help/forms/using/embed-adaptive-form-aem-sites.md) AEM Sites o in una pagina Web ospitata all’esterno di AEM. Il modulo adattivo incorporato è completamente funzionante e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente all&#39;utente di restare nel contesto di altri elementi della pagina Web e di interagire contemporaneamente con il modulo.

## Prerequisiti {#prerequisites}

Effettuare le seguenti operazioni prima di incorporare un modulo adattivo in un sito Web esterno

* Pubblicate il modulo adattivo da incorporare nell’istanza pubblica del server AEM Forms.
* Create o identificate una pagina Web nel sito Web in cui è ospitato il modulo adattivo. Verificate che la pagina Web sia in grado di [leggere i file jQuery da un CDN](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js) o che disponga di una copia locale del file jQuery incorporato. jQuery è richiesto per eseguire il rendering di un modulo adattivo.
* Quando il server AEM e la pagina Web si trovano su domini diversi, eseguite i passaggi elencati nella sezione, [abilitate i AEM Forms a distribuire moduli adattivi a un sito](#cross-site)interdominio.

## Incorpora modulo adattivo {#embed-adaptive-form}

È possibile incorporare un modulo adattivo inserendo alcune righe di JavaScript nella pagina Web. L’API nel codice invia una richiesta HTTP al server AEM per risorse di moduli adattivi e inserisce il modulo adattivo nel contenitore di moduli specificato.

Per incorporare il modulo adattivo:

1. Create una pagina Web sul sito Web con il seguente codice:

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

   * Modificate il valore della variabile *options.path* con il percorso dell’URL di pubblicazione del modulo adattivo. Se il server AEM è in esecuzione su un percorso contestuale, accertati che l’URL includa il percorso contestuale. Ad esempio, il codice riportato sopra e l&#39;adattatore risiedono sullo stesso server di moduli AEM, pertanto nell&#39;esempio viene utilizzato il percorso contestuale del modulo adattivo /content/forms/af/locbasic.html.
   * Sostituisci *options.dataRef* con gli attributi da trasmettere con l’URL. È possibile utilizzare la variabile dataref per [precompilare un modulo](/help/forms/using/prepopulate-adaptive-form-fields.md)adattivo.
   * Sostituisci *options.subjectPath* con il percorso a un tema diverso dal tema configurato nel modulo adattivo. In alternativa, potete specificare il percorso del tema utilizzando l&#39;attributo request.
   * CSS_Selector è il selettore CSS del contenitore di moduli in cui è incorporato il modulo adattivo. Ad esempio, la classe css .customafsection è il selettore CSS nell&#39;esempio precedente.

Il modulo adattivo è incorporato nella pagina Web. Osservate quanto segue nel modulo adattivo incorporato:

* L&#39;intestazione e il piè di pagina del modulo adattivo originale non sono inclusi nel modulo incorporato.
* Le bozze e i moduli inviati sono disponibili nella scheda Bozze e invii del portale Forms.
* L&#39;azione di invio configurata sul modulo adattivo originale viene mantenuta nel modulo incorporato.
* Le regole dei moduli adattivi vengono mantenute e completamente funzionanti nel modulo incorporato.
* Il targeting delle esperienze e i test A/B configurati nel modulo adattivo originale non funzionano nel modulo incorporato.
* Se Adobe  Analytics è configurato sul modulo originale, i dati di analisi vengono acquisiti nel server Adobe  Analytics. Tuttavia, non è disponibile nel rapporto di analisi Moduli.

## Topologia di esempio {#sample-topology}

La pagina Web esterna che incorpora il modulo adattivo invia le richieste al server AEM, che in genere si trova dietro il firewall in una rete privata. Per garantire che le richieste siano indirizzate in modo sicuro al server AEM, si consiglia di configurare un server proxy inverso.

Vediamo un esempio di come impostare un server proxy inverso Apache 2.4 senza dispatcher. In questo esempio, ospiterai il server AEM con il percorso `/forms` contestuale e mapperai `/forms` il proxy inverso. In questo modo tutte le richieste `/forms` sul server Apache vengono indirizzate all’istanza AEM. Questa topologia consente di ridurre il numero di regole nel livello del dispatcher, poiché tutte le richieste hanno il prefisso `/forms` route al server AEM.

1. Aprite il file di `httpd.conf` configurazione e rimuovete il commento dalle seguenti righe di codice. In alternativa, è possibile aggiungere queste righe di codice nel file.

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. Configurate le regole del proxy aggiungendo le seguenti righe di codice nel file di `httpd-proxy.conf` configurazione.

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   Sostituisci `[AEM_Instance`] con l’URL di pubblicazione del server AEM presente nelle regole.

Se non installi il server AEM su un percorso contestuale, le regole del proxy sul livello Apache saranno le seguenti:

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
>Se configurate un’altra topologia, accertatevi di aggiungere gli URL di invio, precompilazione e altri URL al inserire nell&#39;elenco Consentiti  del livello del dispatcher.

## Best practices {#best-practices}

Durante l&#39;incorporazione di un modulo adattivo in una pagina Web, tenere in considerazione le procedure ottimali seguenti:

* Assicurarsi che le regole di stile definite nella pagina Web CSS non siano in conflitto con l&#39;oggetto modulo CSS. Per evitare i conflitti, potete riutilizzare il CSS della pagina Web nel tema del modulo adattivo utilizzando la libreria client AEM. Per informazioni sull&#39;utilizzo della libreria client nei temi dei moduli adattivi, vedere [Temi in AEM Forms](../../forms/using/themes.md).
* Per fare in modo che il contenitore del modulo nella pagina Web utilizzi l’intera larghezza della finestra. Garantisce il funzionamento delle regole CSS configurate per i dispositivi mobili senza alcuna modifica. Se il contenitore del modulo non occupa l&#39;intera larghezza della finestra, è necessario scrivere CSS personalizzato per adattare il modulo ai diversi dispositivi mobili.
* Utilizzare `[getData](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` l&#39;API per ottenere la rappresentazione XML o JSON dei dati del modulo nel client.
* Utilizzate `[unloadAdaptiveForm](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API per scaricare il modulo adattivo dal DOM HTML.
* Configurate l’intestazione access-control-origin quando inviate la risposta dal server AEM.

## Abilitare i AEM Forms per distribuire moduli adattivi a un sito interdominio {#cross-site}

1. Nell’istanza di creazione di AEM, andate a Gestione configurazione console Web AEM all’indirizzo `https://'[server]:[port]'/system/console/configMgr`.
1. Individuate e aprite la configurazione del filtro **** Apache Sling Referrer.
1. Nel campo Host consentiti, specificate il dominio in cui risiede la pagina Web. Consente all’host di effettuare richieste POST al server AEM. È inoltre possibile utilizzare l&#39;espressione regolare per specificare una serie di domini applicazione esterni.

