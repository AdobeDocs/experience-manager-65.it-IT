---
title: Tipi di moduli interfaccia utente ContextHub di esempio
seo-title: Tipi di moduli interfaccia utente ContextHub di esempio
description: ContextHub offre diversi moduli di interfaccia utente di esempio utilizzabili nelle soluzioni
seo-description: ContextHub offre diversi moduli di interfaccia utente di esempio utilizzabili nelle soluzioni
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 1%

---


# Tipi di moduli interfaccia utente ContextHub di esempio {#sample-contexthub-ui-module-types}

ContextHub offre diversi moduli di interfaccia utente di esempio che è possibile utilizzare nelle soluzioni. Vengono fornite le seguenti informazioni:

* Le principali funzioni del modulo dell’interfaccia utente.
* Dove trovare il codice sorgente per aprirlo a scopo di apprendimento.
* Come configurare il modulo dell’interfaccia utente.

Per informazioni sull’aggiunta di moduli dell’interfaccia utente a ContextHub, consultate [Aggiunta di un modulo](ch-configuring.md#adding-a-ui-module)dell’interfaccia utente. Per informazioni sullo sviluppo di moduli di interfaccia utente, consultate [Creazione di tipi](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)di moduli di interfaccia utente ContextHub.

## tipo di modulo interfaccia utente contexthub.base {#contexthub-base-ui-module-type}

Il tipo di modulo dell’interfaccia utente contexthub.base è il tipo di base per tutti gli altri tipi di moduli dell’interfaccia utente. Fornisce pertanto funzionalità generiche per il rendering dei dati dell&#39;archivio.

Sono disponibili le seguenti funzioni:

* **Titolo e icona:** Specificate un titolo per il modulo dell’interfaccia utente e un’icona. È possibile fare riferimento all&#39;icona utilizzando un URL o dalla libreria delle icone dell&#39;interfaccia utente Coral.
* **Archivia dati:** Identificare uno o più store da cui recuperare i dati.
* **Contenuto:** Specificate il contenuto che viene visualizzato nel modulo dell&#39;interfaccia utente così come viene visualizzato nella barra degli strumenti ContextHub.
* **Contenuto poster:** Specificate il contenuto che viene visualizzato in un contenitore quando si fa clic o si tocca il modulo dell&#39;interfaccia utente.
* **Modalità a schermo intero:** Controllare se la modalità a schermo intero è consentita.

Il codice sorgente si trova in /libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js.

### Configurazione {#configuration}

Configurate il modulo dell&#39;interfaccia utente contexthub.base utilizzando un oggetto Javascript in formato JSON. Per configurare le funzioni del modulo dell’interfaccia utente, includete una delle seguenti proprietà:

* **image:** URL di un&#39;immagine da visualizzare come icona.
* **icona:** Il nome di una classe di icone [dell&#39;interfaccia utente](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) Coral. Se specificate un valore per le proprietà dell&#39;icona e dell&#39;immagine, l&#39;immagine viene utilizzata.

* **title:** Titolo per il modulo dell’interfaccia utente. Il titolo viene visualizzato quando il puntatore viene messo in pausa sull&#39;icona del modulo dell&#39;interfaccia utente.
* **fullscreen:** Valore booleano che indica se il modulo dell&#39;interfaccia utente supporta la modalità a schermo intero. Utilizzare `true` per supportare la modalità a schermo intero e `false` per impedire la modalità a schermo intero.

* **modello:** Modello [Handlebars](https://handlebarsjs.com/) che specifica il contenuto da eseguire il rendering nella barra degli strumenti ContextHub. Utilizzate al massimo due `<p>` tag.

* **storeMapping:** Mappatura chiave/store. Utilizzate la chiave nei modelli Handlebar per accedere ai dati dell&#39;archivio ContextHub associati.
* **elenco:** Un array di elementi da visualizzare come elenco in un puntatore quando si fa clic sul modulo dell&#39;interfaccia utente. Se includete questo elemento, non includete possverTemplate. Il valore è un array di oggetti con le seguenti chiavi:

   * title: Testo da visualizzare per l&#39;elemento
   * image: (Facoltativo) URL di un&#39;immagine che deve essere visualizzata a sinistra
   * icona: (Facoltativo) Una classe di icone CUI da visualizzare a sinistra; ignorato se viene specificata un&#39;immagine
   * selezionato: (Facoltativo) Un valore booleano che specifica se l&#39;elemento deve essere visualizzato come selezionato (true=selezionato). Per impostazione predefinita, gli elementi selezionati vengono visualizzati in grassetto. Utilizzare una `listType` proprietà per configurare altri aspetti (vedere di seguito).

* **listType:** Stile da utilizzare per le voci dell&#39;elenco di contenitori. Utilizzate uno dei seguenti valori:

   * segno di spunta
   * Casella
   * radio

* **poverTemplate:** Un modello Handlebars che specifica il contenuto da eseguire nel puntatore quando si fa clic sul modulo dell&#39;interfaccia utente. Se includete questo elemento, non includete l&#39; `list` elemento.

### Esempio {#example}

L’esempio seguente configura un modulo dell’interfaccia utente contexthub.base per visualizzare informazioni provenienti da uno store [contexthub.emulators](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) . L&#39; `template` elemento illustra come ottenere i dati dallo store utilizzando la chiave stabilita dall&#39; `storeMapping` elemento.

```xml
{
   "icon": "coral-Icon--move",
    "title": "Screen Resolution",
    "storeMapping": {
      "emulator": "emulators"
    },
    "template": "<p>{{{ i18n \"Resolution\"}}}</p><p>{{{emulator.currentDevice.width}}} x {{{emulator.currentDevice.height}}}</p>"
}
```

![chlimage_1-76](assets/chlimage_1-76a.png)

## tipo di modulo interfaccia utente contexthub.browserinfo {#contexthub-browserinfo-ui-module-type}

Il modulo dell&#39;interfaccia utente contexthub.browserinfo visualizza informazioni sul browser Web del client e sul sistema operativo. Le informazioni sono ottenute dal negozio surferinfo, in base al candidato [contexthub.surferinfo](/help/sites-developing/ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) .

![chlimage_1-77](assets/chlimage_1-77a.png)

Il codice sorgente per il modulo dell’interfaccia utente si trova in /libs/granite/contexthub/components/module/browserinfo. Anche se contexthub.browserinfo estende il modulo dell’interfaccia utente contexthub.base, esso non esclude né fornisce funzioni aggiuntive. L&#39;implementazione fornisce una configurazione predefinita per il rendering delle informazioni del browser.

### Configurazione {#configuration-1}

Le istanze del modulo di interfaccia utente contexthub.browserinfo non richiedono un valore per la configurazione dei dettagli. Il seguente testo JSON rappresenta la configurazione predefinita del modulo.

```xml
{
   "icon":"coral-Icon--globe",
   "title":"Browser/OS Information",
   "storeMapping":{"surferinfo":"surferinfo"},
   "template":"<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p><p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>"
}
```

## tipo di modulo interfaccia utente contexthub.datetime {#contexthub-datetime-ui-module-type}

Il modulo dell’interfaccia utente contexthub.datetime visualizza la data e l’ora memorizzate in uno store denominato datetime basato sul candidato dell’archivio [contexthub.datetime](/help/sites-developing/ch-samplestores.md#contexthub-datetime-sample-store-candidate) .

![chlimage_1-78](assets/chlimage_1-78a.png)

Il modulo fornisce un modulo per la verifica che consente di modificare la data e l&#39;ora nello store.

L’origine del modulo dell’interfaccia utente contexthub.datetime si trova in /libs/granite/contexthub/components/module/datetime.

### Configurazione {#configuration-2}

Le istanze del modulo dell’interfaccia utente contexthub.datetime non richiedono un valore per la configurazione dei dettagli. Il seguente testo JSON rappresenta la configurazione predefinita del modulo.

```xml
{
   "icon":"coral-Icon--clock",
   "title":"DATE&TIME",
   "clickable":true,
   "storeMapping":{"d":"datetime"},
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"Date&Time\"}}</p><p class=\"contexthub-module-line2\">{{d.formatted.locale.date}} {{d.formatted.locale.time}}</p>",
   "popoverTemplate":"<div class=\"datetime center\"><div class=\"coral-DatePicker-calendar\" data-init=\"datepicker\"><input class=\"coral-Textfield\" type=\"datetime\" value=\"{{d.formatted.iso}}\"><button class=\"coral-Button coral-Button--secondary coral-Button--square\" title=\"{{i18n \"Datetime picker\"}}\"><i class=\"coral-Icon coral-Icon--calendar coral-Icon--sizeS\"></i></button></div></div>"
}
```

## tipo di modulo interfaccia utente contexthub.location {#contexthub-location-ui-module-type}

Il modulo dell’interfaccia utente contexthub.location visualizza la longitudine e la latitudine del client. Il modulo fornisce un contenitore che mostra una mappa Google su cui potete fare clic per cambiare la posizione corrente. Il modulo ottiene le informazioni da uno store ContextHub denominato geolocation basato sul candidato [contexthub.geolocation](/help/sites-developing/ch-samplestores.md#contexthub-geolocation-sample-store-candidate) .

![chlimage_1-80](assets/chlimage_1-80a.png)

L’origine del modulo dell’interfaccia utente si trova in /etc/cloudsettings/default/contexthub/geolocation.

### Configurazione {#configuration-4}

Le istanze del modulo dell’interfaccia utente contexthub.location non richiedono un valore per la configurazione dei dettagli. Il seguente testo JSON rappresenta la configurazione predefinita del modulo.

```xml
{
 "icon":"coral-Icon--compass",
 "title":"Location",
 "clickable":true,
 "editable":{"key":"/geolocation","disabled":[],"hidden":["/geolocation/generatedThumbnail","/geolocation/city","/geolocation/country"]},
 "fullscreen":true,
 "storeMapping":{"g":"geolocation"},
 "template":"<p>{{i18n \"Location\"}}</p><p>{{g.address.postalCode}} {{g.address.city}}{{#if g.address.city}}{{#if g.address.region}},{{/if}}{{/if}} {{g.address.region}}</p>",
 "list":[
  {"title":"Basel, Switzerland",
  "data":{"longitude":7.58929,"latitude":47.554746,"city":"Basel","country":"Switzerland"}},
  {"title":"Melbourne, Australia",
  "data":{"longitude":144.96328,"latitude":-37.814107,"city":"Melbourne","country":"Australia"}},
  {"title":"Beijing, China",
  "data":{"longitude":116.407526,"latitude":39.90403,"city":"Beijing","country":"China"}},
  {"title":"New York, NY, USA",
  "data":{"longitude":-74.005973,"latitude":40.714353,"city":"New York","country":"United States"}},
  {"title":"Paris, France",
  "data":{"longitude":2.352222,"latitude":48.856614,"city":"Paris","country":"France"}},
  {"title":"Rio de Janeiro, Brazil",
  "data":{"longitude":-43.20071,"latitude":-22.913395,"city":"Rio","country":"Brazil"}},
  {"title":"San Jose, CA, USA",
  "data":{"longitude":-121.894955,"latitude":37.339386,"city":"San Jose","country":"United States"}},
  {"title":"Tokyo, Japan",
  "data":{"longitude":139.691706,"latitude":35.689487,"city":"Shinjuku","country":"Japan"}}
 ],
 "listType":"checkmark"
}
```

## contexthub.screen-orientation UI Module Type {#contexthub-screen-orientation-ui-module-type}

Il modulo dell&#39;interfaccia utente di orientamento contexthub.screen visualizza l&#39;orientamento dello schermo corrente del client. Anche se disabilitato per impostazione predefinita, il modulo fornisce un puntatore che consente di selezionare un orientamento. Il modulo ottiene informazioni da uno store ContextHub denominato emulatori basato sul candidato [granite.emulators](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) .

![chlimage_1-81](assets/chlimage_1-81a.png)

L’origine del modulo dell’interfaccia utente si trova in /libs/granite/contexthub/components/module/screen-orientation.

### Configurazione {#configuration-5}

Le istanze del modulo dell’interfaccia utente di orientamento contexthub.screen non richiedono un valore per la configurazione dei dettagli. Il seguente testo JSON rappresenta la configurazione predefinita del modulo. Tenere presente che la `clickable` proprietà è `false` per impostazione predefinita. Se si ignora la configurazione predefinita da impostare `clickable` su `true`, facendo clic sul modulo viene visualizzata una finestra a comparsa in cui è possibile selezionare l&#39;orientamento.

```xml
{
   "icon":"coral-Icon--rotateRight",
   "title":"Screen Orientation",
   "clickable":false,
   "storeMapping":{"emulator":"emulators"},
   "template":"<p>{{{ i18n \"Screen Orientation\" }}}</p><p>{{{ emulator.currentDevice.orientation }}}",
   "listReference":"/emulators/orientations",
   "listType":"checkmark"
}
```

## tipo di modulo interfaccia utente contexthub.tagcloud {#contexthub-tagcloud-ui-module-type}

Il modulo dell’interfaccia utente contestexthub.tagcloud presenta informazioni sui tag. Sulla barra degli strumenti, il modulo dell’interfaccia utente mostra il numero di tag. La finestra a comparsa presenta un tag cloud e una casella di testo per l’aggiunta di nuovi tag. Il modulo dell’interfaccia utente ottiene informazioni da uno store ContextHub denominato tagcloud basato sul candidato per lo store [contexthub.tagcloud](/help/sites-developing/ch-samplestores.md#contexthub-tagcloud-sample-data-store) .

![chlimage_1-82](assets/chlimage_1-82a.png)

L’origine del modulo dell’interfaccia utente si trova in /libs/granite/contexthub/components/module/tagcloud.

### Configurazione {#configuration-6}

Le istanze del modulo di interfaccia utente contexthub.tagcloud non richiedono un valore per la configurazione dei dettagli. Il seguente testo JSON rappresenta la configurazione predefinita del modulo.

```xml
{
   "icon":"coral-Icon--tag",
   "title":"TagCloud",
   "clickable":true,
   "storeMapping":{"t":"tagcloud"},
   "maxTags":20,
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"TagCloud\"}}</p><p class=\"contexthub-module-line2\">{{stats.total}} {{i18n \"Tags\"}}</p>",
   "popoverTemplate":"<div class=\"contexthub-popover-content center\"><p class=\"stats\">{{stats.total}} {{i18n \"Tags\"}} | {{stats.hits}} {{i18n \"Hits\"}} | {{i18n \"Last tag\"}}: {{#if stats.recent}}{{stats.recent}}{{else}}{{i18n \"Unknown\"}}{{/if}}</p><p class=\"tagcloud\">{{#each tags}}<span class=\"tag{{this.weight}}\">{{this.name}}</span> {{/each}}</p><div class=\"coral-InputGroup\"><input type=\"text\" class=\"coral-InputGroup-input coral-Textfield tag-name\" placeholder=\"{{i18n \"Add a namespace:my/tag\"}}\" pattern=\"^[A-Za-z0-9_\\-]+(:[A-Za-z0-9_\\-\\/]+)?$\" title=\"{{i18n \"namespace:my/tag\"}}\"><span class=\"coral-InputGroup-button\"><button class=\"coral-Button coral-Button--secondary coral-Button--square contexthub-new-tag\" type=\"button\" title=\"{{i18n \"increment\"}}\"><i class=\"coral-Icon coral-Icon--sizeS coral-Icon--add\"></i></button></span></div></div>"
}
```

## tipo di modulo granite.profile UI {#granite-profile-ui-module-type}

Il modulo dell&#39;interfaccia utente ContextHub granite.profile visualizza il nome visualizzato dell&#39;utente corrente. La finestra a comparsa mostra il nome di accesso dell&#39;utente e consente di modificare il valore del nome visualizzato. Il modulo dell’interfaccia utente ottiene informazioni da uno store ContextHub denominato profile basato sul candidato per lo store [granite.profile](/help/sites-developing/ch-samplestores.md#granite-profile-sample-store-candidate) .

![chlimage_1-83](assets/chlimage_1-83a.png)

L’origine del modulo dell’interfaccia utente è /libs/granite/contexthub/components/module/profile.

### Configurazione {#configuration-7}

Le istanze del modulo grantie.profile UI non richiedono un valore per la configurazione dei dettagli. Il seguente testo JSON rappresenta la configurazione predefinita del modulo.

```xml
{
   "icon":"coral-Icon--user",
   "title":"Profile",
   "clickable":true,
   "editable":{
      "key":"/profile",
      "disabled":["/profile/authorizableId"],
      "hidden":["/profile/avatar","/profile/path"]},
   "storeMapping":{"p":"profile"},
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"Persona\"}}</p><p class=\"contexthub-module-line2\">{{p.displayName}}</p>",
   "listType":"checkmark"
}
```
