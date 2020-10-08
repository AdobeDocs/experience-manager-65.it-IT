---
title: Helper manubrio SCF
seo-title: Helper manubrio SCF
description: Metodi helper handlebars per facilitare l’utilizzo di SCF
seo-description: Metodi helper handlebars per facilitare l’utilizzo di SCF
uuid: 9c514199-871e-4b68-8147-2052d2eeda15
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8b6c1697-d693-41f4-8337-f41658465107
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 2%

---


# Helper manubrio SCF {#scf-handlebars-helpers}

| **[⇐ Funzioni Essenziali](essentials.md)** | **[Personalizzazione lato server ⇒](server-customize.md)** |
|---|---|
|  | **[Personalizzazione lato client ⇒](client-customize.md)** |

Gli Helpers (helper) sono metodi richiamabili dagli script Handlebars per facilitare l’utilizzo dei componenti SCF.

L&#39;implementazione include una definizione lato client e lato server. È inoltre possibile per gli sviluppatori creare helper personalizzati.

Gli assistenti SCF personalizzati forniti con  AEM Communities sono definiti nella libreria [client](../../help/sites-developing/clientlibs.md):

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>Accertatevi di installare il pacchetto [di funzioni Community](deploy-communities.md#latestfeaturepack)più recente.

## Abbreviate {#abbreviate}

Un helper che restituisce una stringa abbreviata conforme alle proprietà maxWords e maxLength.

La stringa da abbreviare viene fornita come contesto. Se non viene fornito alcun contesto, viene restituita una stringa vuota.

Innanzitutto, il contesto viene troncato su maxLength, quindi il contesto viene suddiviso in parole e ridotto a maxWords.

Se safeString è impostato su true, la stringa restituita è una SafeString.

### Parametri {#parameters}

* **contesto**: Stringa

   (Facoltativo) Il valore predefinito è la stringa vuota

* **maxLength**: Numero

   (Facoltativo) Il valore predefinito corrisponde alla lunghezza del contesto.

* **maxWords**: Numero

   (Facoltativo) Il valore predefinito è il numero di parole nella stringa tagliata.

* **safeString**: Booleano

   (Facoltativo) Restituisce un Handlebars.SafeString() se true. Il valore predefinito è false.

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

Un helper per per aggiungere due estensioni sotto un div, una per il testo completo e l&#39;altra per il testo minore, con la possibilità di alternare tra le due viste.

### Parametri {#parameters-1}

* **contesto**: Stringa

   (Facoltativo) Il valore predefinito è la stringa vuota.

* **numChars**: Numero

   (Facoltativo) Il numero di caratteri da visualizzare quando non viene visualizzato il testo completo. Il valore predefinito è 100.

* **moreText**: Stringa

   (Facoltativo) Il testo da visualizzare che indica che vi è più testo da visualizzare. Il valore predefinito è &quot;more&quot;.

* **ellipsesText**: Stringa

   (Facoltativo) Il testo da visualizzare che indica la presenza di testo nascosto. Il valore predefinito è &quot;..&quot;.

* **safeString**: Booleano

   (Facoltativo) Valore booleano che indica se applicare o meno Handlebars.SafeString() prima di restituire il risultato. Il valore predefinito è false.

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

Assistenza per restituire una stringa data formattata.

### Parametri {#parameters-2}

* **contesto**: Numero

   (Facoltativo) un valore di scostamento millisecondi dal 1 gennaio 1970 (epoch). Il valore predefinito è la data corrente.

* **formato**: Stringa

   (Facoltativo) Formato della data da applicare. Il valore predefinito è &quot;AAAA-MM-DDTHH:mm:ss.sssZ&quot; e il risultato viene visualizzato come &quot;2015-03-18T18:17:13-07:00&quot;

### Esempi {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## Equals {#equals}

Un helper per restituire il contenuto in base a una condizione di uguaglianza.

### Parametri {#parameters-3}

* **lvalue**: Stringa

   Il valore a sinistra da confrontare.

* **rvalue**: Stringa

   Il valore a destra da confrontare.

### Esempio {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
{{else}}
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm-mode {#if-wcm-mode}

Supporto per blocchi che verifica il valore corrente della modalità [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) WCM rispetto a un elenco di modalità separate da stringhe.

### Parametri {#parameters-4}

* **contesto**: Stringa

   (Facoltativo) Stringa da tradurre. Obbligatorio se non viene fornito alcun valore predefinito.

* **modalità**: Stringa

   (Facoltativo) Elenco separato da virgole delle modalità [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) WCM da verificare se impostato.

### Esempio {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{{else}}
 ...
{{/if-wcm-mode}}
```

## i18n {#i-n}

Questo helper sostituisce l&#39;helper Handlebars &#39;i18n&#39;.

Vedere anche [Internazionalizzazione delle stringhe nel codice](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code)JavaScript.

### Parametri {#parameters-5}

* **contesto**: Stringa

   (Facoltativo) Stringa da tradurre. Obbligatorio se non viene fornito alcun valore predefinito.

* **predefinito**: Stringa

   (Facoltativo) Stringa predefinita da tradurre. Obbligatorio se non viene fornito alcun contesto.

* **commento**: Stringa

   (Facoltativo) Suggerimento per la traduzione

### Esempio {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## Includi {#include}

Supporto per includere un componente come risorsa non esistente in un modello.

Questo consente di personalizzare la risorsa in modo programmatico più facilmente di quanto sia possibile per una risorsa aggiunta come nodo JCR. Consultate [Aggiungere o includere un componente](scf.md#add-or-include-a-communities-component)Community.

Sono inclusi solo alcuni componenti Community. Per AEM 6.1, quelli che possono essere inclusi sono [commenti](essentials-comments.md), [valutazioni](rating-basics.md), [revisioni](reviews-basics.md)e [votazioni](essentials-voting.md).

Questo helper, appropriato solo sul lato server, fornisce funzionalità simili a [cq:include](../../help/sites-developing/taglib.md) per gli script JSP.

### Parametri {#parameters-6}

* **contesto**: Stringa o oggetto

   (Facoltativo, a meno che non venga fornito un percorso relativo)

   Utilizzare `this` per trasmettere il contesto corrente.

   Utilizzare `this.id` per ottenere la risorsa in corrispondenza `id` del quale eseguire il rendering resourceType richiesto.

* **resourceType**: Stringa

   (Facoltativo) Per impostazione predefinita, il tipo di risorsa viene impostato sul tipo di risorsa dal contesto.

* **modello**: Stringa

   Percorso dello script del componente.

* **percorso**: Stringa

   (Obbligatorio) Percorso della risorsa. Se il percorso è relativo, è necessario fornire un contesto, altrimenti viene restituita la stringa vuota.

* **authoringDisabled**: Booleano

   (Facoltativo) Il valore predefinito è false. Solo per uso interno.

### Esempio {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

Questo includerà un nuovo componente Commenti in `this.id` + /commenti.

## IncludeClientLib {#includeclientlib}

Un helper che include una libreria client HTML AEM, che può essere un js, un css o una libreria di temi. Per più inclusioni di tipi diversi, ad esempio js e css, questo tag deve essere utilizzato più volte nello script Handlebars.

Questo helper, appropriato solo sul lato server, fornisce funzionalità simili a [ui:includeClientLib](../../help/sites-developing/taglib.md) per gli script JSP.

### Parametri {#parameters-7}

* **categorie**: Stringa

   (Facoltativo) Elenco di categorie di lib client separate da virgole. Questo includerà tutte le librerie Javascript e CSS per le categorie indicate. Il nome del tema viene estratto dalla richiesta.

* **tema**: Stringa

   (Facoltativo) Elenco di categorie di lib client separate da virgole. Questo includerà tutte le librerie correlate ai temi (sia CSS che JS) per le categorie indicate. Il nome del tema viene estratto dalla richiesta.

* **js**: Stringa

   (Facoltativo) Elenco di categorie di lib client separate da virgole. Questo includerà tutte le librerie Javascript per le categorie indicate.

* **css**: Stringa

   (Facoltativo) Elenco di categorie di lib client separate da virgole. Questo includerà tutte le librerie CSS per le categorie specificate.

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

## Tempo utile {#pretty-time}

Un helper per per visualizzare il tempo passato a un punto di interruzione, dopo il quale viene visualizzato un formato di data regolare.

Esempio:

* 12 ore fa
* 7 giorni fa

### Parametri {#parameters-8}

* **contesto**: Numero

   Un&#39;ora in passato per paragonare a &#39;ora&#39;. Il tempo è espresso come valore di scostamento millisecondi dal 1 gennaio 1970 (epoch).

* **DaysCutoff**: Numero

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

Un helper che codifica una stringa di origine per il contenuto dell&#39;elemento HTML per proteggere da XSS.

NOTA: non è un validatore e non deve essere utilizzato per scrivere i valori degli attributi.

### Parametri {#parameters-9}

* **contesto**: object

   L’HTML da codificare.

### Esempio {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

Un helper che codifica una stringa di origine per la scrittura in un valore attributo HTML per proteggere da XSS.

NOTA: non è un validatore e non deve essere utilizzato per scrivere attributi utilizzabili (href, src, gestori di eventi).

### Parametri {#parameters-10}

* **contesto**: Oggetto

   L’HTML da codificare.

### Esempio {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

Helper che codifica una stringa di origine per la scrittura nel contenuto di stringa JavaScript per proteggere da XSS.

NOTA: non è un validatore e non deve essere utilizzato per scrivere in JavaScript arbitrari.

### Parametri {#parameters-11}

* **contesto**: Oggetto

   L’HTML da codificare.

### Esempio {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

Un helper che rimuove un URL per la scrittura come valore di attributo di tipo HREF o srce HTML per proteggere XSS.

NOTA: potrebbe restituire una stringa vuota

### Parametri {#parameters-12}

* **contesto**: Oggetto

   URL da rimuovere.

### Esempio {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Handlebars.js Panoramica di base {#handlebars-js-basic-overview}

Panoramica rapida delle funzioni di supporto dalla documentazione [](https://handlebarsjs.com/expressions.html)Handlebars.js:

* Una chiamata dell&#39;helper Handlebars è un identificatore semplice (il *nome* dell&#39;helper), seguito da zero o più parametri separati da spazio.
* I parametri possono essere un semplice oggetto String, number, boolean o JSON, così come una sequenza facoltativa di coppie chiave-valore (argomenti hash) come ultimo parametro/i.
* Le chiavi negli argomenti hash devono essere identificatori semplici.
* I valori negli argomenti hash sono espressioni Handlebars: identificatori semplici, percorsi o stringhe.
* Il contesto corrente, `this`, è sempre disponibile per gli assistenti Handlebars.
* Il contesto può essere un oggetto dati String, number, boolean o JSON.
* È possibile trasmettere un oggetto nidificato nel contesto corrente come contesto, ad esempio `this.url` o `this.id` (vedere gli esempi seguenti di assistenti di blocco e semplici).

* I blocchetti helper sono funzioni che possono essere richiamate da qualsiasi punto del modello. Possono richiamare un blocco del modello zero o più volte con un contesto diverso ogni volta. Contengono un contesto tra {{#*name*}} e {{/*name*}}.

* Handlebars fornisce un parametro finale agli helper denominati &#39;options&#39;. L&#39;oggetto speciale &quot;options&quot; include

   * Dati privati facoltativi (options.data)
   * Proprietà chiave-valore facoltative dalla chiamata (options.hash)
   * Possibilità di richiamare se stesso (options.fn()
   * Possibilità di richiamare l&#39;inverso di se stesso (options.inverse()

* È consigliabile che il contenuto della stringa HTML restituito da un helper sia una SafeString.

### Un esempio di semplice helper dalla documentazione di Handlebars.js: {#an-example-of-a-simple-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link_to', function(title, options) {
    return new Handlebars.SafeString('<a href="/posts' + this.url + '">' + title + "!</a>");
});

var context = {posts: [
    {url: "/hello-world",
      body: "Hello World!"}
  ] };

// when link_to is called, posts is the current context
var source = '<ul>{{#posts}}<li>{{{link_to "Post"}}}</li>{{/posts}}</ul>'

var template = Handlebars.compile(source);

template(context);
```

Rendering:

&lt;ul>&lt;li>&lt;a href=&quot;/post/hello-world&quot;>Post!&lt;/a>&lt;/li>&lt;/ul>

### Esempio di supporto per blocchi dalla documentazione di Handlebars.js: {#an-example-of-a-block-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link', function(options) {
    return new Handlebars.SafeString('<a href="/people/' + this.id + '">' + options.fn(this) + '</a>');
});

var data = { "people": [
  { "name": "Alan", "id": 1 },
  { "name": "Yehuda", "id": 2 }
]};

// when link is called, people is the current context
var source = "<ul>{{#people}}<li>{{#link}}{{name}}{{/link}}</li>{{/people}}</ul>";

var template = Handlebars.compile(source);

template(data);
```

Rendering:
&lt;ul>&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>&lt;li>&lt;a href=&quot;/people/2&quot;>Yehuda&lt;/a>&lt;/li>&lt;/ul>

## Helper SCF personalizzati {#custom-scf-helpers}

I client helper personalizzati devono essere implementati sia sul lato server che sul lato client, soprattutto quando si passano i dati. Per gli SCF, la maggior parte dei modelli vengono compilati e sottoposti a rendering sul lato server, poiché il server genera l’HTML per un determinato componente quando la pagina viene richiesta.

### Helper personalizzati lato server {#server-side-custom-helpers}

Per implementare e registrare un helper SCF personalizzato sul lato server, implementate semplicemente l&#39;interfaccia Java [TemplateHelper](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html), rendetelo un servizio [](../../help/sites-developing/the-basics.md#osgi) OSGi e installatelo come parte di un bundle OSGi.

Esempio:

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
>È inoltre necessario creare un helper creato per il lato server per il lato client.
>
>Il componente viene riprodotto sul lato client per l’utente che ha eseguito l’accesso e, se l’helper sul lato client non viene trovato, il componente scompare.

### Helper personalizzati lato client {#client-side-custom-helpers}

Gli assistenti lato client sono script Handlebars registrati mediante chiamata `Handlebars.registerHelper()`.
Esempio:

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

Gli helper personalizzati lato client devono essere aggiunti a una libreria client personalizzata.
clientlib deve:

* Includi una dipendenza in `cq.social.scf`.
* Caricamento dopo il caricamento di Handlebars.
* Sia [incluso](clientlibs.md).

Nota: gli assistenti SCF sono definiti in `/etc/clientlibs/social/commons/scf/helpers.js`.

| **[⇐ Funzioni Essenziali](essentials.md)** | **[Personalizzazione lato server ⇒](server-customize.md)** |
|---|---|
|  | **[Personalizzazione lato client ⇒](client-customize.md)** |

