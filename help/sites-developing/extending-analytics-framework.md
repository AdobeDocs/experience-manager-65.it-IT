---
title: Personalizzazione di  Adobe Analytics Framework
seo-title: Personalizzazione di  Adobe Analytics Framework
description: 'null'
seo-description: 'null'
uuid: 444a29c2-3b4e-4d21-adc0-5f317ece2b77
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 11c0aac6-a7f6-4d6b-a080-b04643045a64
translation-type: tm+mt
source-git-commit: 0dc96f07e45ccbfea4edc87431677ada5b1bfa8c
workflow-type: tm+mt
source-wordcount: '1620'
ht-degree: 0%

---


# Personalizzazione di Adobe Analytics Framework {#customizing-the-adobe-analytics-framework}

Il framework Adobe Analytics  determina le informazioni tracciate con  Adobe Analytics. Per personalizzare il framework predefinito, utilizzate javascript per aggiungere il tracciamento personalizzato, integrare  plug-in Adobe Analytics e modificare le impostazioni generali nel framework utilizzato per il tracciamento.

## Informazioni su JavaScript generato per Framework {#about-the-generated-javascript-for-frameworks}

Quando una pagina è associata a un framework Adobe Analytics  e include [riferimenti al modulo Analytics](/help/sites-administering/adobeanalytics.md), per la pagina viene generato automaticamente un file analytics.sitecatalyst.js.

javascript nella pagina crea un oggetto `s_gi`definito dalla libreria Adobe Analytics s_code.js  assegna valori alle relative proprietà. Il nome dell&#39;istanza dell&#39;oggetto è `s`. Gli esempi di codice presentati in questa sezione fanno diversi riferimenti a questa variabile `s`.

Il codice di esempio seguente è simile al codice presente in un file analytics.sitecatalyst.js:

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";

/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

Quando utilizzate codice JavaScript personalizzato per personalizzare il framework, modificate il contenuto di questo file.

## Configurazione  proprietà Adobe Analytics {#configuring-adobe-analytics-properties}

All&#39;interno  Adobe Analytics sono presenti numerose variabili predefinite configurabili in un framework. Le variabili **charset**, **cookieLifetime**, **currencyCode** e **trackInlineStats** sono incluse per impostazione predefinita nell&#39;elenco **Impostazioni generali di Analytics**.

![aa-22](assets/aa-22.png)

È possibile aggiungere i nomi e i valori delle variabili all&#39;elenco. Queste variabili predefinite ed eventuali variabili aggiunte vengono utilizzate per configurare le proprietà dell&#39;oggetto `s` nel file analytics.sitecatalyst.js. L&#39;esempio seguente mostra come la proprietà `prop10` aggiunta di valore `CONSTANT` sia rappresentata nel codice javascript:

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.prop10= 'CONSTANT';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";
```

Per aggiungere variabili all&#39;elenco, attenersi alla procedura descritta di seguito.

1. Nella pagina  framework Adobe Analytics, espandete l&#39;area **Impostazioni generali di Analytics**.
1. Sotto l’elenco delle variabili, fate clic su Aggiungi elemento per aggiungere una nuova variabile all’elenco.
1. Nella cella a sinistra, immettere un nome per la variabile, ad esempio `prop10`.

1. Nella colonna di destra, inserite un valore per la variabile, ad esempio `CONSTANT`.

1. Per rimuovere una variabile, fare clic sul pulsante (-) accanto alla variabile.

>[!NOTE]
>
>Quando si immettono variabili e valori, assicurarsi che siano formattati e digitati correttamente oppure che le chiamate **non vengano inviate** con la coppia di valori/variabili corretta. Le variabili e i valori errati possono anche impedire l’esecuzione di chiamate.
>
>Per verificare che queste variabili siano impostate correttamente, rivolgetevi al rappresentante Adobe Analytics .

>[!CAUTION]
>
>Alcune delle variabili in questo elenco sono **obbligatorie** per consentire il corretto funzionamento  chiamate Adobe Analytics (ad es. **currencyCode**, **charSet**)
>
>Quindi, anche se vengono rimossi dal framework stesso, saranno comunque associati con un valore predefinito quando viene effettuata la chiamata Adobe Analytics .

### Aggiunta di JavaScript personalizzato a un  Adobe Analytics Framework {#adding-custom-javascript-to-an-adobe-analytics-framework}

La casella javascript gratuita nell&#39;area **Impostazioni generali di Analytics** consente di aggiungere codice personalizzato a un framework Adobe Analytics .

![a-21](assets/aa-21.png)

Il codice aggiunto viene aggiunto al file analytics.sitecatalyst.js. Pertanto, è possibile accedere alla variabile `s`, che è un&#39;istanza dell&#39;oggetto javascript `s_gi` definito in `s_code.js`. Ad esempio, l&#39;aggiunta del codice seguente equivale all&#39;aggiunta di una variabile denominata `prop10` di valore `CONSTANT`, come illustrato nella sezione precedente:

`s.prop10= 'CONSTANT';`

Il codice nel file [analytics.sitecatalyst.js](/help/sites-developing/extending-analytics-components.md) (che include il contenuto del  file Adobe Analytics `s-code.js`) contiene il codice seguente:

`if (s.usePlugins) s.doPlugins(s)`

La procedura seguente illustra come utilizzare la casella javascript per personalizzare  tracciamento Adobe Analytics. Se il javascript deve utilizzare  plug-in Adobe Analytics, [integrarli](/help/sites-administering/adobeanalytics.md) in AEM.

1. Aggiungete il seguente codice javascript alla casella in modo da eseguire `s.doPlugins`:

   ```
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom code here
   }
   s.doPlugins=s_doPlugins;
   ```

   >[!CAUTION]
   >
   >Questo codice è necessario se desiderate inviare variabili in una chiamata Adobe Analytics  che sono state personalizzate in un modo che non può essere fatto tramite l’interfaccia di trascinamento di base OPPURE attraverso JavaScript in linea in  vista Adobe Analytics.
   >
   >Se le variabili personalizzate non rientrano nella funzione s_doPlugins, verranno inviate come *undefined *nella chiamata Adobe Analytics 

1. Aggiungete il codice javascript nella funzione **s_doPlugins**.

Nell&#39;esempio seguente vengono concatenati i dati acquisiti in una pagina in ordine gerarchico, utilizzando un separatore comune di &quot;|&quot;.

Un framework Adobe Analytics  dispone delle seguenti configurazioni:

* La variabile Adobe Analytics `prop2`  è mappata sulla proprietà del sito `pagedata.sitesection`.

* La variabile Adobe Analytics `prop3`  è mappata sulla proprietà del sito `pagedata.subsection`.

* Il codice seguente è aggiunto alla casella javascript gratuita:

   ```
   s.usePlugins=true;
    function s_doPlugins(s) {
    s.prop1 = s.prop2+'|'+s.prop3;
    }
    s.doPlugins=s_doPlugins;
   ```

* Quando viene visualizzata la pagina Web che utilizza il framework (o, in modalità di modifica, la pagina viene ricaricata o visualizzata in anteprima), vengono eseguite le chiamate a  Adobe Analytics.

Ad esempio, in  Adobe Analytics vengono generati i seguenti valori:

![aa-20](assets/aa-20.png)

### Aggiunta di codice personalizzato globale per tutti i  Adobe Analytics Framework {#adding-global-custom-code-for-all-adobe-analytics-frameworks}

Fornite codice JavaScript personalizzato integrato in tutti i framework Adobe Analytics . Quando il framework Adobe Analytics  pagina non contiene un codice JavaScript [a forma libera ](/help/sites-administering/adobeanalytics.md) personalizzato, il codice javascript generato dallo script /libs/cq/analytics/components/sitecatalyst/config.js.jsp viene aggiunto al file [analytics.sitecatalyst.js](/help/sites-administering/adobeanalytics.md). Per impostazione predefinita, lo script non ha alcun effetto perché è impostato come commento. Il codice imposta anche `s.usePlugins` su `false`:

```
/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

Il codice nel file analytics.sitecatalyst.js (che include il contenuto del file  Adobe Analytics s_code.js) contiene il codice seguente:

if (s.usePlugins) s.doPlugins(s)

Pertanto, il codice JavaScript deve essere impostato su `s.usePlugins` in modo che venga eseguito qualsiasi codice della funzione `s_doPlugins`. `true` Per personalizzare il codice, sovrapponete il file config.js.jsp con uno che utilizza il vostro javascript. Se il javascript deve utilizzare  plug-in Adobe Analytics, [integrarli](/help/sites-administering/adobeanalytics.md) in AEM.

>[!NOTE]
>
>Non modificate il file /libs/cq/analytics/components/sitecatalyst/config.js.jsp. Alcune AEM attività di aggiornamento o manutenzione possono reinstallare il file originale, rimuovendo le modifiche.

1. In CRXDE Lite , create la struttura di cartelle /apps/cq/analytics/components:

   1. Fate clic con il pulsante destro del mouse sulla cartella /apps e fate clic su Crea > Crea cartella.
   1. Specificate `cq` come nome della cartella e fate clic su OK.
   1. Allo stesso modo, create le cartelle `analytics` e `components`.

1. Fare clic con il pulsante destro del mouse sulla cartella `components` appena creata e scegliere Crea > Crea componente. Specificate i seguenti valori di proprietà:

   * Etichetta: `sitecatalyst`
   * Titolo: `sitecatalyst`
   * Super Type: `/libs/cq/analytics/components/sitecatalyst`
   * Gruppo: `hidden`

1. Fare clic più volte su Avanti finché il pulsante OK non è attivato, quindi fare clic su OK.

   Il componente sitecatalyst contiene il file sitecatalyst.jsp creato automaticamente.

1. Fate clic con il pulsante destro del mouse sul file sitecatalyst.jsp e fate clic su Elimina.

1. Fate clic con il pulsante destro del mouse sul componente SiteCatalyst e fate clic su Crea > Crea file. Specificate il nome `config.js.jsp`, quindi fate clic su OK.

   Il file config.js.jsp si apre automaticamente per la modifica.

1. Aggiungete il testo seguente al file, quindi fate clic su Salva tutto:

   ```java
   <%@page session="true"%>
   /* Plugin Config */
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom plugin code here
   }
   s.doPlugins=s_doPlugins;
   ```

   Il codice JavaScript generato dallo script /apps/cq/analytics/components/sitecatalyst/config.js.jsp ora viene inserito nel file analytics.sitecatalyst.js per tutte le pagine che utilizzano un framework Adobe Analytics .

1. Aggiungete il codice JavaScript da eseguire nella funzione `s_doPlugins`, quindi fate clic su Salva tutto.

>[!CAUTION]
>
>Se un testo è presente nello javascript a forma libera del framework di una pagina (anche solo spazi bianchi), config.js.jsp viene ignorato.

### Utilizzo  plug-in Adobe Analytics in AEM {#using-adobe-analytics-plugins-in-aem}

Ottenete il codice javascript per  i plug-in Adobe Analytics e integrateli nel framework Adobe Analytics  in AEM. Aggiungete il codice a una cartella libreria client della categoria `sitecatalyst.plugins` in modo che sia disponibile per il codice JavaScript personalizzato.

Ad esempio, se si integra il plug-in `getQueryParams`, è possibile richiamare il plug-in dalla funzione `s_doPlugins` del javascript personalizzato. Il seguente codice di esempio invia la stringa di query in **&quot;pid&quot;** dall&#39;URL del referente come **eVar1**, quando viene attivata una chiamata Adobe Analytics .

```
s.usePlugins=true;
function s_doPlugins(s) {
   // take the query string from the referrer
   s.eVar1=s.getQueryParam('pid','',document.referrer);
}
s.doPlugins=s_doPlugins;
```

AEM i seguenti  plug-in Adobe Analytics, in modo che siano disponibili per impostazione predefinita:

* getQueryParam()
* getPreviousValue()
* split()

La cartella della libreria client /libs/cq/analytics/clientlibs/sitecatalyst/plugins include questi plug-in nella categoria sitecatalyst.plugins.

>[!NOTE]
>
>Create una nuova cartella libreria client per i plug-in. Non aggiungere plug-in alla cartella `/libs/cq/analytics/clientlibs/sitecatalyst/plugins`. In questo modo il contributo alla categoria `sitecatalyst.plugins` non verrà sovrascritto durante AEM reinstallazione o le attività di aggiornamento.

Utilizzate la procedura seguente per creare la cartella della libreria client per i plug-in. È necessario eseguire questa procedura solo una volta. Per aggiungere un plug-in alla cartella della libreria client, utilizzate la procedura seguente.

1. In un browser Web, aprite CRXDE Lite. ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))

1. Fate clic con il pulsante destro del mouse sulla cartella /apps/my-app/clientlibs e scegliete Crea > Crea nodo. Immettete i seguenti valori di proprietà e fate clic su OK:

   * Nome: Un nome per la cartella della libreria client, ad esempio i miei plug-in

   * Tipo: cq:ClientLibraryFolder

1. Selezionate la cartella della libreria client appena creata e utilizzate la barra delle proprietà in basso a destra per aggiungere la seguente proprietà:

   * Nome: category
   * Tipo: Stringa
   * Valore: sitecatalyst.plugins
   * Multi: selected

   Fare clic su OK nella finestra Modifica per confermare il valore della proprietà.

1. Fate clic con il pulsante destro del mouse sulla cartella della libreria client appena creata e fate clic su Crea > Crea file. Per il nome del file digitare js.txt, quindi fare clic su OK.

1. Fate clic su Salva tutto.

Utilizzate la procedura seguente per ottenere il codice plug-in, memorizzare il codice nell&#39;archivio AEM e aggiungere il codice alla cartella della libreria client.

1. Accedete a [sc.omniture.com](https://sc.omniture.com) utilizzando il vostro account Adobe Analytics .
1. Nella pagina di destinazione, accedete a Aiuto > Home dell’Aiuto.
1. Nel sommario a sinistra, fate clic su Plug-in di implementazione.
1. Fate clic sul collegamento al plug-in che desiderate aggiungere e quando la pagina si apre, individuate il codice sorgente javascript per il plug-in, quindi selezionate il codice e copiatelo.

1. Fate clic con il pulsante destro del mouse sulla cartella della libreria client e fate clic su Crea > Crea file. Per il nome del file, digitate il nome del plug-in che state integrando seguito da .js, quindi fate clic su OK. Ad esempio, se state integrando il plug-in getQueryParam, assegnate al file il nome getQueryParam.js.

   Quando create il file, questo viene aperto per la modifica.

1. Incollate il codice JavaScript del plug-in nel file, fate clic su Salva tutto, quindi chiudete il file.

1. Aprite il file js.txt dalla cartella della libreria client.

1. In una nuova riga, aggiungete il nome del file che contiene il plug-in, ad esempio getQueryParam.js. Quindi, fate clic su Salva tutto e chiudete il file.

>[!NOTE]
>
>Quando si utilizzano i plug-in, assicurarsi di integrare anche eventuali plugin di supporto, altrimenti il plugin javascript non riconoscerà le chiamate che effettua alle funzioni nel plugin di supporto. Ad esempio, il plug-in getPreviousValue() richiede che il plug-in split() funzioni correttamente.
>
>Il nome del plug-in di supporto deve essere aggiunto anche a **js.txt**.
