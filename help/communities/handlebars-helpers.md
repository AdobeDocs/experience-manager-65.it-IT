---
title: Helper Handlebars SCF
description: Handlebars Helper metodi per facilitare il lavoro con SCF
topic-tags: developing
content-type: reference
exl-id: bfb95cae-4b0f-4521-a113-042dc4005a63
source-git-commit: 787e5a87f13498006e2ce897e85ee12704b58f09
workflow-type: tm+mt
source-wordcount: '1453'
ht-degree: 2%

---

# Helper Handlebars SCF {#scf-handlebars-helpers}

| **[⇐ funzioni di base](essentials.md)** | **[⇒ di personalizzazione lato server](server-customize.md)** |
|---|---|
|   | **[⇒ di personalizzazione lato client](client-customize.md)** |

Handlebars Helpers (helpers) sono metodi richiamabili dagli script Handlebars per facilitare l’utilizzo dei componenti SCF.

L’implementazione include una definizione lato client e lato server. È inoltre possibile per gli sviluppatori creare helper personalizzati.

Gli helper SCF personalizzati forniti con AEM Communities sono definiti nel [libreria client](../../help/sites-developing/clientlibs.md):

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>Assicurarsi di installare [feature pack più recente per Communities](deploy-communities.md#latestfeaturepack).

## Abbrevia {#abbreviate}

Helper per restituire una stringa abbreviata conforme alle proprietà maxWords e maxLength.

La stringa da abbreviare viene fornita come contesto. Se non viene fornito alcun contesto, viene restituita una stringa vuota.

Innanzitutto, il contesto viene ridotto a maxLength, quindi viene suddiviso in parole e ridotto a maxWords.

Se safeString è impostato su true, la stringa restituita sarà una stringa provvisoria.

### Parametri {#parameters}

* **contesto**: Stringa

  (Facoltativo) Il valore predefinito è la stringa vuota

* **maxLength**: numero

  (Facoltativo) Il valore predefinito è la lunghezza del contesto.

* **maxWords**: numero

  (Facoltativo) Il valore predefinito è il numero di parole nella stringa tagliata.

* **safeString**: booleano

  (Facoltativo) Restituisce un valore Handlebars.SafeString() se true. Il valore predefinito è false.

### Esempi {#examples}

```
{{abbreviate subject maxWords=2}}

/*
If subject =
    "AEM Communities - Site Creation Wizard"

Then abbreviate would return
    "AEM Communities".
*/
```

```
{{{abbreviate message safeString=true maxLength=30}}}

/*
If message =
    "The goal of AEM Communities is to quickly create a community engagement site."

Then abbreviate would return
    "The goal of AEM Communities is"
*/
```

## Content-loadmore {#content-loadmore}

Un helper per aggiungere due estensioni sotto un div, una per il testo completo e l’altra per il testo meno, con la possibilità di passare da una visualizzazione all’altra.

### Parametri {#parameters-1}

* **contesto**: Stringa

  (Facoltativo) Il valore predefinito è la stringa vuota.

* **numChars**: numero

  (Facoltativo) Il numero di caratteri da visualizzare quando non viene visualizzato il testo completo. Il valore predefinito è 100.

* **moreText**: Stringa

  (Facoltativo) Testo da visualizzare per indicare che è presente altro testo da visualizzare. Il valore predefinito è &quot;more&quot;.

* **ellipsesText**: Stringa

  (Facoltativo) Testo da visualizzare che indica la presenza di testo nascosto. Il valore predefinito è &quot;...&quot;.

* **safeString**: booleano

  (Facoltativo) Valore booleano che indica se applicare Handlebars.SafeString() prima di restituire il risultato. Il valore predefinito è false.

### Esempio {#example}

```
{{content-loadmore  context numChars=32  moreText="go on"  ellipsesText="..." }}

/*
If context =
    "Here is the initial less content and this is more content."

Then content-loadmore would return
    "Here is the initial less content<span class="moreelipses">...</span> <span class="scf-morecontent"><span>and this is more content.</span>  <a href="" class="scf-morelink" evt="click=toggleContent">go on</a></span>"
*/
```

## DateUtil {#dateutil}

Un helper per restituire una stringa di data formattata.

### Parametri {#parameters-2}

* **contesto**: numero

  (Facoltativo) offset di un valore in millisecondi dal 1 gennaio 1970 (epoca). Il valore predefinito è la data corrente.

* **formato**: Stringa

  (Facoltativo) Il formato della data da applicare. Il valore predefinito è &quot;YYYY-MM-DDTHH:mm:ss.sssZ&quot; e il risultato appare come &quot;2015-03-18T18:17:13-07:00&quot;

### Esempi {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## Uguale a {#equals}

Un helper per restituire il contenuto a seconda di un condizionale di uguaglianza.

### Parametri {#parameters-3}

* **lvalue**: Stringa

  Valore di sinistra da confrontare.

* **rvalue**: Stringa

  Valore di destra da confrontare.

### Esempio {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
`{{else}}`
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm-mode {#if-wcm-mode}

Un helper di blocco che verifica il valore corrente di [Modalità WCM](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) in un elenco di modalità separato da stringhe.

### Parametri {#parameters-4}

* **contesto**: Stringa

  (Facoltativo) Stringa da tradurre. Obbligatorio se non viene fornito alcun valore predefinito.

* **modalità**: Stringa

  (Facoltativo) Un elenco separato da virgole di [Modalità WCM](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) per eseguire il test se impostato.

### Esempio {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{else}}
 ...
`{{/if-wcm-mode}}`
```

## i18n {#i-n}

Questo helper sostituisce l&#39;helper Handlebars &#39;i18n&#39;.

Vedi anche [Internazionalizzazione delle stringhe nel codice JavaScript](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code).

### Parametri {#parameters-5}

* **contesto**: Stringa

  (Facoltativo) Stringa da tradurre. Obbligatorio se non viene fornito alcun valore predefinito.

* **predefinito**: Stringa

  (Facoltativo) Stringa predefinita da tradurre. Obbligatorio se non viene fornito alcun contesto.

* **commento**: Stringa

  (Facoltativo) Un suggerimento per la traduzione

### Esempio {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## Includi {#include}

Un helper per includere un componente come risorsa non esistente in un modello.

Questo metodo consente di personalizzare la risorsa a livello di programmazione più facilmente di quanto non sia possibile per una risorsa aggiunta come nodo JCR. Consulta [Aggiungere o includere un componente community](scf.md#add-or-include-a-communities-component).

Sono disponibili solo alcuni componenti di Communities da includere. <!-- OBSOLETE/OLD  NEED TO UPDATE FOR 6.5  For AEM 6.1, those that are includable are [comments](essentials-comments.md), [rating](rating-basics.md), [reviews](reviews-basics.md), and [voting](essentials-voting.md). -->

Questo helper, appropriato solo sul lato server, offre funzionalità simili a [cq:include](../../help/sites-developing/taglib.md) per gli script JSP.

### Parametri {#parameters-6}

* **contesto**: stringa o oggetto

  (Facoltativo, a meno che non fornisca un percorso relativo)

  Utilizzare `this` per trasmettere il contesto corrente.

  Utilizzare `this.id` per ottenere la risorsa da `id` per il rendering del resourceType richiesto.

* **resourceType**: Stringa

  (Facoltativo) il tipo di risorsa viene impostato automaticamente sul tipo di risorsa dal contesto.

* **modello**: Stringa

  Percorso dello script del componente.

* **percorso**: Stringa

  (Obbligatorio) Percorso della risorsa. Se il percorso è relativo, è necessario fornire un contesto, altrimenti viene restituita la stringa vuota.

* **authoringDisabled**: booleano

  (Facoltativo) Il valore predefinito è false. Solo per uso interno.

### Esempio {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

Include un nuovo componente commenti in `this.id` + /comments

## IncludeClientLib {#includeclientlib}

Helper che include una libreria client HTML AEM, che può essere una libreria js, css o theme. Per più inclusioni di tipi diversi, ad esempio js e css, questo tag deve essere utilizzato più volte nello script Handlebars.

Questo helper, appropriato solo sul lato server, offre funzionalità simili a [ui:includeClientLib](../../help/sites-developing/taglib.md) per gli script JSP.

### Parametri {#parameters-7}

* **categorie**: Stringa

  (Facoltativo) Un elenco di categorie di librerie client separate da virgole. Includi tutte le librerie JavaScript e CSS per le categorie specificate. Il nome del tema viene estratto dalla richiesta.

* **tema**: Stringa

  (Facoltativo) Un elenco di categorie di librerie client separate da virgole. Includi tutte le librerie relative al tema (sia CSS che JS) per le categorie specificate. Il nome del tema viene estratto dalla richiesta.

* **js**: Stringa

  (Facoltativo) Un elenco di categorie di librerie client separate da virgole. Include tutte le librerie JavaScript per le categorie specificate.

* **css**: Stringa

  (Facoltativo) Un elenco di categorie di librerie client separate da virgole. Include tutte le librerie CSS per le categorie specificate.

### Esempi {#examples-2}

```
// all: js + theme (theme-js + css)
{{includeClientLib categories="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/socialgraph.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/socialgraph.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// only js libs
{{includeClientLib js="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/socialgraph.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// theme only (theme-js + css)
{{includeClientLib theme="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// css only
{{includeClientLib css="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/socialgraph.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
```

## Bel tempo {#pretty-time}

Un helper per visualizzare il tempo trascorso fino a un punto di interruzione, dopo il quale viene visualizzato un formato di data regolare.

Ad esempio:

* 12 ore fa
* 7 giorni fa

### Parametri {#parameters-8}

* **contesto**: numero

  Un periodo nel passato da confrontare con &quot;adesso&quot;. Il tempo è espresso come valore in millisecondi con offset dal 1 gennaio 1970 (epoca).

* **daysCutoff**: numero

  Il numero di giorni fa prima del passaggio a una data effettiva. Il valore predefinito è 60.

### Esempio {#example-5}

```
{{pretty-time this.published daysCutoff=7}}

/*
Depending on how long in the past, may return

  "3 minutes ago"

  "3 hours ago"

  "3 days ago"
*/
```

## Xss-html {#xss-html}

Helper che codifica una stringa di origine per il contenuto dell’elemento HTML per evitare attacchi XSS.

NOTA: questo helper non è un validatore e non deve essere utilizzato per la scrittura di valori di attributo.

### Parametri {#parameters-9}

* **contesto**: oggetto

  HTML da codificare.

### Esempio {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

Helper che codifica una stringa di origine per la scrittura in un valore di attributo HTML per evitare attacchi XSS.

NOTA: questo helper non è un validatore e non deve essere utilizzato per scrivere attributi utilizzabili (href, src, gestori eventi).

### Parametri {#parameters-10}

* **contesto**: oggetto

  HTML da codificare.

### Esempio {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

Helper che codifica una stringa di origine per la scrittura di contenuti di stringhe JavaScript per evitare attacchi XSS.

NOTA: questo helper non è un validatore e non deve essere utilizzato per la scrittura in JavaScript arbitrario.

### Parametri {#parameters-11}

* **contesto**: oggetto

  HTML da codificare.

### Esempio {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

Helper che bonifica un URL per la scrittura come valore di attributo HTML href o di risorsa per proteggersi da XSS.

NOTA: questo helper potrebbe restituire una stringa vuota.

### Parametri {#parameters-12}

* **contesto**: oggetto

  URL da bonificare.

### Esempio {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Panoramica di base di Handlebars.js {#handlebars-js-basic-overview}

* Una chiamata helper Handlebars è un identificatore semplice (il *nome* dell&#39;helper), seguito da zero o più parametri separati da spazi.
* I parametri possono essere un semplice oggetto String, number, booleano o JSON e una sequenza facoltativa di coppie chiave-valore (argomenti hash) come ultimi parametri.
* Le chiavi negli argomenti hash devono essere identificatori semplici.
* I valori negli argomenti hash sono espressioni Handlebars: identificatori semplici, percorsi o stringhe.
* Il contesto attuale, `this`, è sempre disponibile per gli assistenti Handlebars.
* Il contesto può essere un oggetto dati String, number, booleano o JSON.
* È possibile passare come contesto un oggetto nidificato all’interno del contesto corrente, ad esempio `this.url` o `this.id` (vedi gli esempi seguenti di helper semplici e a blocchi).

* Gli helper di blocco sono funzioni che possono essere richiamate da qualsiasi punto del modello. Possono richiamare un blocco del modello zero o più volte con un contesto diverso ogni volta. Contengono un contesto tra `{{#*name*}}` e `{{/*name*}}`.

* Handlebars fornisce un parametro finale agli helper chiamato &#39;options&#39;. L’oggetto speciale &quot;options&quot; include

   * Dati privati facoltativi (options.data)
   * Proprietà chiave-valore facoltative dalla chiamata (options.hash)
   * Possibilità di richiamarsi (options.fn())
   * Possibilità di richiamare l’inverso di se stesso (options.inverse())

* È consigliabile che il contenuto della stringa HTML restituito da un helper sia un SafeString.

### Un esempio di un semplice helper dalla documentazione di Handlebars.js: {#an-example-of-a-simple-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link_to', function(title, options) {
    return new Handlebars.SafeString('<a href="/posts' + this.url + '">' + title + "!</a>");
});

var context = {posts: [
    {url: "/hello-world",
      body: "Hello World!"}
  ] };

// when link_to is called, posts is the current context
var source = '<ul>`{{#posts}}`<li>{{{link_to "Post"}}}</li>`{{/posts}}`</ul>'

var template = Handlebars.compile(source);

template(context);
```

Esegue il rendering:

&lt;ul>
&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>Pubblica!&lt;/a>&lt;/li>
&lt;/ul>

### Un esempio di helper per blocchi tratto dalla documentazione di Handlebars.js: {#an-example-of-a-block-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link', function(options) {
    return new Handlebars.SafeString('<a href="/people/' + this.id + '">' + options.fn(this) + '</a>');
});

var data = { "people": [
  { "name": "Alan", "id": 1 },
  { "name": "Yehuda", "id": 2 }
]};

// when link is called, people is the current context
var source = "<ul>`{{#people}}`<li>`{{#link}}``{{name}}``{{/link}}`</li>`{{/people}}`</ul>";

var template = Handlebars.compile(source);

template(data);
```

Esegue il rendering:
&lt;ul>
&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>
&lt;li>&lt;a href=&quot;/people/2&quot;>Yehuda&lt;/a>&lt;/li>
&lt;/ul>

## Helper SCF personalizzati {#custom-scf-helpers}

Gli helper personalizzati devono essere implementati sul lato server e sul lato client, soprattutto durante il trasferimento dei dati. Per l&#39;SCF, la maggior parte dei modelli viene compilata e riprodotta sul lato server mentre il server genera le HTML per un determinato componente quando la pagina viene richiesta.

### Helper personalizzati lato server {#server-side-custom-helpers}

Per implementare e registrare un helper SCF personalizzato sul lato server, è sufficiente implementare l’interfaccia Java™ [TemplateHelper](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html), rendilo un [Servizio OSGi](../../help/sites-developing/the-basics.md#osgi) e installarlo come parte di un bundle OSGi.

Ad esempio:

### FooTextHelper.java {#footexthelper-java}

```java
/** Custom Handlebars Helper */

package com.my.helpers;

import java.io.IOException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

import com.adobe.cq.social.handlebars.api.TemplateHelper;
import com.github.jknack.handlebars.Options;

@Service
@Component
public class FooTextHelper implements TemplateHelper<String>{

    @Override
    public CharSequence apply(String context, Options options) throws IOException {
        return "foo-" + context;
    }

    @Override
    public String getHelperName() {
        return "foo-text";
    }

    @Override
    public Class<String> getContextType() {
        return String.class;
    }
}
```

>[!NOTE]
>
>È necessario creare un helper creato per il lato server anche per il lato client.
>
>Il componente viene nuovamente sottoposto a rendering sul lato client per l’utente connesso e, se l’helper lato client non viene trovato, il componente scompare.

### Helper personalizzati lato client {#client-side-custom-helpers}

Gli helper lato client sono script Handlebars registrati richiamando `Handlebars.registerHelper()`.
Ad esempio:

### custom-helpers.js {#custom-helpers-js}

```
function(Handlebars, SCF, $CQ) {

    Handlebars.registerHelper('foo-text', function(context, options) {
        if (!context) {
            return "";
        }
        return "foo-" + context;
    });

})(Handlebars, SCF, $CQ);
```

Gli helper lato client personalizzati devono essere aggiunti a una libreria client personalizzata.
La libreria client deve:

* Includi una dipendenza da `cq.social.scf`.
* Carica dopo il caricamento di Handlebars.
* Essere [incluso](clientlibs.md).

Nota: gli helper SCF sono definiti in `/etc/clientlibs/social/commons/scf/helpers.js`.

| **[⇐ funzioni di base](essentials.md)** | **[⇒ di personalizzazione lato server](server-customize.md)** |
|---|---|
|   | **[⇒ di personalizzazione lato client](client-customize.md)** |
