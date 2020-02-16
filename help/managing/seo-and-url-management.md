---
title: Best practice per SEO e gestione degli URL
seo-title: Best practice per SEO e gestione degli URL
description: Scopri le best practice e le raccomandazioni SEO per ottenere questi risultati con un’implementazione AEM.
seo-description: Scopri le best practice e le raccomandazioni SEO per ottenere questi risultati con un’implementazione AEM.
uuid: 943e76c4-bd88-4b52-bb43-db375eb89d23
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 7c8f2cec-870b-41a8-8d98-70e29b495587
docset: aem65
translation-type: tm+mt
source-git-commit: c623724df8d849f4cc01f5dc134c775dc24dafc7

---


# Best practice per SEO e gestione degli URL{#seo-and-url-management-best-practices}

L’ottimizzazione SEO (Search Engine Optimization, ottimizzazione motore di ricerca) è diventata una preoccupazione fondamentale per molti esperti di marketing. Di conseguenza, i dubbi relativi al SEO devono essere risolti in molti progetti AEM.

Questo documento descrive innanzitutto alcune best practice [e raccomandazioni](#seo-best-practices) SEO per ottenere questi risultati con un’implementazione AEM. Questo documento approfondisce alcuni dei passaggi [di implementazione più](#aem-configurations) complessi sollevati nella prima sezione.

## Best practice SEO {#seo-best-practices}

Questa sezione descrive alcune best practice generali per il SEO.

### URL {#urls}

Esistono alcune best practice generalmente accettate per gli URL.

Nel progetto AEM, quando valuta gli URL, chiedi:

&quot;Se un utente visualizzasse questo URL e nessuno dei contenuti della pagina, potrebbe descrivere cos&#39;era questa pagina?&quot;

Se la risposta è sì, è probabile che l’URL funzioni correttamente per un motore di ricerca.

Di seguito sono riportati alcuni suggerimenti generali su come creare gli URL per il SEO:

* Utilizzare i trattini per separare le parole.

   * Denominate le pagine utilizzando i trattini (-) come separatori.
   * Evitate di usare cassa in cammello, caratteri di sottolineatura e spazi.

* Evitare l&#39;uso di parametri di query quando possibile. Se necessario, limitateli a due o meno.

   * Utilizzate la struttura di directory per indicare l&#39;architettura delle informazioni, se disponibile.
   * Se una struttura di directory non è un&#39;opzione, utilizzate i selettori Sling nell&#39;URL anziché le stringhe di query. Oltre al valore SEO fornito, i selettori sling rendono anche le pagine memorizzabili nella cache per il dispatcher.

* Più un URL leggibile dall&#39;uomo è, meglio è; se nell’URL sono presenti parole chiave, il valore aumenta.

   * Quando si utilizzano i selettori su una pagina, si preferiscono i selettori che forniscono valori semantici.
   * Se un utente non è in grado di leggere l’URL, non può farlo nemmeno un motore di ricerca.
   * Esempio:
      `mybrand.com/products/product-detail.product-category.product-name.html`
è preferito a `mybrand.com/products/product-detail.1234.html`

* Evita i sottodomini quando possibile, in quanto i motori di ricerca li tratteranno come entità diverse, frammentando il valore SEO del sito.

   * Utilizzate invece percorsi secondari di primo livello. Ad esempio, anziché `es.mybrand.com/home.html`, utilizzare `www.mybrand.com/es/home.html`.

   * Pianificate la gerarchia dei contenuti in modo che corrisponda al modo in cui verranno presentati i contenuti, in base a questa linea guida.

* L’efficacia delle parole chiave negli URL diminuisce con l’aumentare della lunghezza dell’URL e della posizione della parola chiave. In altre parole, è meglio accorciare.

   * Utilizzate le tecniche di abbreviazione degli URL e le funzioni fornite da AEM per rimuovere parti URL superflue.
   * Ad esempio, `mybrand.com/en/myPage.html` è preferibile a `mybrand.com/content/my-brand/en/myPage.html`.

* Utilizzate gli URL canonici.

   * Quando un URL può essere servito da percorsi diversi o con parametri o selettori diversi, accertatevi di usare un `rel=canonical` tag sulla pagina.

   * Questo può essere incluso nel codice per il modello AEM.

* Fate corrispondere gli URL ai titoli delle pagine quando possibile.

   * Gli autori dei contenuti dovrebbero essere incoraggiati a seguire questa pratica.

* Supporto dell’insensibilità alle maiuscole/minuscole nelle richieste URL.

   * Configura il dispatcher per riscrittura di tutte le richieste in entrata come lettere minuscole.
   * Gli autori dei contenuti formativi possono creare tutte le pagine utilizzando lettere minuscole.

* Accertatevi che ogni pagina sia servita solo da un protocollo.

   * A volte i siti vengono serviti `http` fino a quando l&#39;utente non raggiunge una pagina, ad esempio con un modulo di estrazione o di login, al quale passa `https`. Quando si collega da questa pagina, se l&#39;utente può tornare alle `http` `https`pagine e accedervi tramite, il motore di ricerca le tiene traccia come due pagine separate.

   * Google attualmente preferisce `https` le pagine a `http` quelle. Per questo motivo spesso rende la vita di tutti più facile servire l&#39;intero sito `https`.

### Server configuration {#server-configuration}

In termini di configurazione del server, potete effettuare le seguenti operazioni per garantire che venga effettuata la ricerca per indicizzazione solo del contenuto corretto:

* Utilizzare un `robots.txt` file per bloccare la ricerca per indicizzazione di qualsiasi contenuto che non deve essere indicizzato.

   * Bloccare **tutte** le operazioni di ricerca per indicizzazione negli ambienti di test.

* Quando avviate un nuovo sito con URL aggiornati, implementate i reindirizzamenti 301 per assicurare che la classificazione SEO esistente non vada perduta.
* Includete un&#39;icona preferita per il sito.
* Implementate una mappa del sito XML per semplificare la ricerca per indicizzazione del contenuto da parte dei motori di ricerca. Accertatevi di includere una mappa del sito mobile per siti mobili e/o reattivi.

## Configurazioni AEM {#aem-configurations}

Questa sezione descrive i passaggi di implementazione necessari per configurare AEM in modo che segua queste raccomandazioni SEO.

### Utilizzo dei selettori Sling {#using-sling-selectors}

Precedentemente, l&#39;uso dei parametri di query era la pratica generalmente accettata durante la creazione di un&#39;applicazione Web aziendale.

Negli ultimi anni, la tendenza è stata quella di rimuovere tali URL nel tentativo di rendere gli URL più leggibili. Su molte piattaforme, questo comporta l’implementazione di reindirizzamenti sul server Web o sulla rete di distribuzione dei contenuti (CDN), ma Sling lo rende semplice. Selettori Sling:

* Maggiore leggibilità degli URL.
* Consente di memorizzare le pagine nella cache del dispatcher e di migliorare spesso la sicurezza.
* Consentono di indirizzare il contenuto direttamente, anziché utilizzare un servlet generico per il recupero del contenuto. Ciò offre i vantaggi degli ACL applicati all&#39;archivio e ai filtri applicati al dispatcher.

#### Utilizzo dei selettori per i servlet {#using-selectors-for-servlets}

AEM offre due opzioni per la scrittura di servlet:

* **bin** servlet
* **Sling** servlet

Gli esempi seguenti illustrano come registrare i servlet che seguono entrambi questi modelli e i vantaggi ottenuti utilizzando i servlet Sling.

#### Servlet del raccoglitore (un livello verso il basso) {#bin-servlets-one-level-down}

**I servlet Bin** seguono il modello a cui molti sviluppatori sono abituati dalla programmazione J2EE. Il servlet viene registrato in un percorso specifico, che nel caso di AEM si trova in genere in `/bin`ed è possibile estrarre i parametri di richiesta necessari dalla stringa di query.

L&#39;annotazione SCR per questo tipo di servlet avrà un aspetto simile al seguente:

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

Estrarre quindi i parametri dalla stringa di query tramite l&#39; `SlingHttpServletRequest` oggetto incluso nel `doGet` metodo; ad esempio:

```
String myParam = req.getParameter("myParam");
```

L’URL risultante usato sarà simile al seguente:

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

Ci sono alcuni punti da considerare con questo approccio:

* L’URL stesso perde il valore SEO. Gli utenti che accedono al sito, inclusi i motori di ricerca, non ricevono alcun valore semantico dall’URL, in quanto l’URL rappresenta un percorso programmatico e non la gerarchia dei contenuti.
* La presenza di parametri di query nell’URL impedisce al dispatcher di memorizzare la risposta nella cache.
* Se si desidera proteggere questo servlet, è necessario implementare la propria logica di sicurezza personalizzata nel servlet.
* Il dispatcher deve essere configurato (attentamente) per essere esposto `/bin/myApp/myServlet`. Esporre semplicemente `/bin` consentirebbe l&#39;accesso a determinati servlet che non dovrebbero essere aperti ai visitatori del sito.

#### Servlet Sling (un livello verso il basso) {#sling-servlets-one-level-down}

**Sling** servlet permette di registrare il servlet in modo opposto. Anziché indirizzare un servlet e specificare il contenuto di cui si desidera eseguire il rendering in base ai parametri di query, occorre indirizzare il contenuto desiderato e specificare il servlet che deve eseguire il rendering del contenuto in base ai selettori Sling.

L&#39;annotazione SCR per questo tipo di servlet avrà un aspetto simile al seguente:

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json”, methods=”GET”)
```

In questo caso, la risorsa che l’URL indirizzi (un’istanza della `myPageType` risorsa) è accessibile automaticamente nel servlet. Per accedervi, chiamate:

```
Resource myPage = req.getResource();
```

L’URL risultante usato sarà simile al seguente:

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

I vantaggi di questo approccio sono:

* Potete cuocere il valore SEO, ottenuto dalla semantica presente nella gerarchia del sito e nel nome della pagina.
* Poiché non sono presenti parametri di query, il dispatcher può memorizzare la risposta nella cache. Inoltre, eventuali aggiornamenti apportati alla pagina indirizzata annulleranno la validità della cache quando la pagina viene attivata.
* Tutti gli ACL applicati `/content/my-brand/my-page` entreranno in vigore quando un utente tenta di accedere al servlet.
* Il dispatcher sarà già configurato per distribuire questo contenuto in funzione della distribuzione del sito Web. Non è richiesta alcuna configurazione aggiuntiva.

### riscrittura URL {#url-rewriting}

In AEM, tutte le pagine Web sono memorizzate in `/content/my-brand/my-content`. Anche se questo può essere utile dal punto di vista della gestione dei dati del repository, non è necessariamente il modo in cui i clienti devono vedere il sito e può entrare in conflitto con le indicazioni SEO per mantenere gli URL il più possibile brevi. È inoltre possibile che vengano utilizzati più siti Web dalla stessa istanza di AEM e da nomi di dominio diversi.

Questa sezione esamina le opzioni disponibili in AEM per gestire questi URL e presentarli agli utenti in modo più leggibile e semplice.

#### Gli URL personalizzati {#vanity-urls}

Se un autore desidera che una pagina sia accessibile da una seconda posizione a scopo promozionale, potrebbe essere utile disporre degli URL personalizzati di AEM, definiti pagina per pagina. Per aggiungere un URL personalizzato a una pagina, accedete alla pagina nella console **Siti** e modificate le proprietà della pagina. Nella parte inferiore della scheda **Base** è disponibile una sezione in cui è possibile aggiungere URL personalizzati. Tenere presente che l’accesso alla pagina tramite più URL frammenterà il valore SEO della pagina, pertanto è necessario aggiungere alla pagina un tag URL canonico per evitare questo problema.

#### Nomi pagina localizzati {#localized-page-names}

È possibile visualizzare i nomi delle pagine localizzate per gli utenti del contenuto convertito. Esempio:

* Anziché consentire a un utente che parla spagnolo di passare a:
   `www.mydomain.com/es/home.html`

* Sarebbe meglio che l’URL fosse:
   `www.mydomain.com/es/casa.html`.

La sfida con la localizzazione del nome della pagina è che molti degli strumenti di localizzazione disponibili sulla piattaforma AEM dipendono dalla corrispondenza dei nomi delle pagine tra diverse lingue per mantenere sincronizzato il contenuto.

La `sling:alias` proprietà permette di avere la nostra torta e mangiarla anche. `sling:alias` può essere aggiunta come proprietà a qualsiasi risorsa per consentire il nome alias della risorsa. Nell&#39;esempio precedente, si dispone di:

* Una pagina nel JCR in:
   `…/es/home`

* Quindi aggiungete una proprietà:
   `sling:alias` = `casa`

In questo modo gli strumenti di traduzione di AEM, come il manager multisito, continueranno a mantenere una relazione tra:

* `/en/home`

* `/es/home`

Consente inoltre agli utenti finali di interagire con il nome della pagina nelle rispettive lingue native.

>[!NOTE]
>
>La `sling:alias` proprietà può essere impostata utilizzando la proprietà [Alias quando si modificano le proprietà](/help/sites-authoring/editing-page-properties.md#advanced)pagina.

#### /etc/map {#etc-map}

In un’installazione standard di AEM:

* per la configurazione OSGi
   **Apache Sling Resource Resolver Factory**( `org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`)

* la proprietà
   **Posizione** mapping ( `resource.resolver.map.location`)

* defaults to `/etc/map`.

Le definizioni di mapping possono essere aggiunte in questa posizione per mappare le richieste in entrata, riscrivere gli URL sulle pagine in AEM o in entrambe.

Per creare una nuova mappatura, create un nuovo `sling:Mapping` nodo in questa posizione in `/http` o `/https`. In base alle proprietà `sling:match` e `sling:internalRedirect` impostate su questo nodo, AEM reindirizzerà tutto il traffico dell’URL corrispondente al valore specificato nella `internalRedirect` proprietà.

Anche se questo è l’approccio documentato nella documentazione ufficiale di AEM e Sling, il supporto delle espressioni regolari fornito da questa implementazione ha un ambito limitato rispetto alle opzioni disponibili utilizzando `SlingResourceResolver` direttamente. Inoltre, l&#39;implementazione delle mappature in questo modo può causare problemi con l&#39;annullamento della validità della cache del dispatcher.

Di seguito è riportato un esempio di come si è verificato il problema:

1. Un utente visita il sito Web e le richieste `https://www.mydomain.com/my-page.html`
1. Il dispatcher inoltra la richiesta al server di pubblicazione.
1. Il server `/etc/map`di pubblicazione risolve la richiesta e ne esegue il rendering `/content/my-brand/my-page` nella pagina.

1. Il dispatcher memorizza nella cache la risposta `/my-page.html` e restituisce la risposta all&#39;utente.
1. Un autore del contenuto apporta una modifica a questa pagina e la attiva.
1. L&#39;agente di eliminazione del dispatcher invia una richiesta di annullamento della validità per `/content/my-brand/my-page`**.**Poiché il dispatcher non ha una pagina memorizzata nella cache in questo percorso, il contenuto precedente rimane memorizzato nella cache e non sarà aggiornato.

Esistono modi per configurare regole di invio personalizzate che mappano l’URL più breve all’URL più lungo a scopo di annullamento della validità della cache.

Tuttavia, esiste anche un modo più semplice per gestire questo:

1. **Regole SlingResourceResolver**

   Utilizzando la console Web (ad esempio, localhost:4502/system/console/configMgr) potete configurare il risolutore risorse Sling:

   * **Apache Sling Resource Resolver Factory**
      `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`.
   È consigliabile creare le mappature necessarie per ridurre gli URL come espressioni regolari, quindi definire queste configurazioni sotto un nodo OsgiConfignode, `config.publish`incluso nella build.

   Invece di definire le mappature in `/etc/map`, queste possono essere assegnate direttamente alle proprietà **URL Mappings** ( `resource.resolver.mapping`):

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   In questo semplice esempio, si sta rimuovendo dall’inizio `/content/my-brand/` di qualsiasi URL dove è presente.

   Questo convertirebbe un URL:

   * from `/content/my-brand/my-page.html`
   * a `/my-page.html`
   Ciò è in linea con la prassi consigliata di mantenere gli URL il più brevi possibile.

1. **Mappatura dell’output URL sulle pagine**

   Dopo aver definito le mappature nel risolutore risorse Apache Sling, è necessario utilizzare queste mappature nei componenti per garantire che gli URL generati sulle pagine siano brevi e ordinati. È possibile farlo utilizzando la funzione mappa del `ResourceResolver`.

   Ad esempio, se state implementando un componente di navigazione personalizzato che elenca gli elementi secondari della pagina corrente, potete utilizzare il metodo di mappatura come segue:

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP Server mod_rewrite {#apache-http-server-mod-rewrite}

Finora, hai implementato mappature insieme alla logica dei tuoi componenti per utilizzare tali mappature durante l’output degli URL sulle nostre pagine.

L&#39;ultimo elemento del puzzle è la gestione di questi URL accorciati quando arrivano al dispatcher, che è il punto in cui `mod_rewrite` vengono riprodotti. Il vantaggio maggiore da utilizzare `mod_rewrite` è che gli URL vengono mappati sul modulo esteso *prima* del loro invio al modulo dispatcher. Questo significa che il dispatcher richiede l’URL lungo dal server di pubblicazione e lo memorizza nella cache di conseguenza. Di conseguenza, qualsiasi richiesta di eliminazione del dispatcher proveniente dal server di pubblicazione sarà in grado di annullare la validità del contenuto.

Per implementare queste regole, potete aggiungere `RewriteRule` elementi sotto l&#39;host virtuale nella configurazione del server Apache HTTP. Se desiderate espandere gli URL abbreviati dell&#39;esempio precedente, potete implementare una regola simile alla seguente:

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### Tag URL canonici {#canonical-url-tags}

I tag URL canonici sono tag di collegamento inseriti nella sezione head di un documento HTML per chiarire in che modo i motori di ricerca devono gestire una pagina durante l&#39;indicizzazione del contenuto. Il vantaggio offerto è di garantire che (versioni diverse di) una pagina venga indicizzata allo stesso modo anche quando l’URL della pagina può contenere delle differenze.

Ad esempio, se un sito offre una versione di una pagina compatibile con la stampante, un motore di ricerca indicizzerebbe tale pagina separatamente dalla versione normale della pagina. Il tag canonico indica al motore di ricerca che sono uguali.

Esempi:

* https://www.mydomain.com/my-brand/my-page.html
* https://www.mydomain.com/my-brand/my-page.print.html

Entrambi applicavano il seguente tag all’intestazione della pagina:

```xml
<link rel=”canonical” href=”my-brand/my-page.html”/>
```

Il valore `href` può essere relativo o assoluto. Il codice deve essere incluso nella marcatura pagina per determinare l’URL canonico per la pagina e generare il tag.

### Configurazione del dispatcher per l’insensibilità ai casi {#configuring-the-dispatcher-for-case-insensitivity}

La procedura ottimale consiste nel distribuire tutte le pagine utilizzando lettere minuscole. Tuttavia, non desiderate che un utente ottenga un 404 quando accede al sito Web utilizzando lettere maiuscole nel proprio URL. Per questo motivo, Adobe consiglia di aggiungere una regola di riscrittura nella configurazione del server Apache HTTP per mappare tutti gli URL in arrivo in lettere minuscole. Inoltre, gli autori dei contenuti devono essere formati per creare le proprie pagine con nomi in lettere minuscole.

Per configurare Apache in modo che tutto il traffico in entrata venga ridotto, aggiungete quanto segue alla `vhost` configurazione:

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

Inoltre, aggiungete quanto segue nella parte superiore del `htaccess` file:

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### Implementazione di robots.txt per proteggere gli ambienti di sviluppo {#implementing-robots-txt-to-protect-development-environments}

I motori di ricerca *devono* verificare la presenza di un `robots.txt` file nella directory principale del sito prima di eseguire il crawling del sito. Dovrebbe essere enfatizzato qui perché mentre i principali motori di ricerca come Google, Yahoo, o Bing tutti rispettano questo, alcuni motori di ricerca stranieri no.

Il modo più semplice per bloccare l&#39;accesso all&#39;intero sito consiste nell&#39;inserire un file denominato `robots.txt` nella directory principale del sito con il seguente contenuto:

```xml
User-agent: *
Disallow: /
```

In alternativa, in un ambiente live, è possibile scegliere di non consentire l&#39;indicizzazione di determinati percorsi.

L&#39;errore di collocare il `robots.txt` file nella directory principale del sito è che le richieste di eliminazione del dispatcher potrebbero cancellare questo file e le mappature URL probabilmente posizioneranno la directory principale del sito in un punto diverso da quello `DOCROOT` definito nella configurazione del server Apache HTTP. Per questo motivo, è comune inserire questo file nell’istanza di creazione nella directory principale del sito e replicarlo nell’istanza di pubblicazione.

### Creazione di un sitemap XML in AEM {#building-an-xml-sitemap-on-aem}

I crawler utilizzano le sitemap XML per comprendere meglio la struttura dei siti Web. Sebbene non vi sia alcuna garanzia che la creazione di un sitemap porti ad un miglioramento delle classificazioni SEO, si tratta di una procedura consigliata concordata. Potete mantenere manualmente un file XML sul server Web da utilizzare come sitemap, ma è consigliabile generare il sitemap a livello di programmazione, in modo che, quando gli autori creano nuovo contenuto, il sitemap rifletta automaticamente le modifiche apportate.

Per generare un sitemap a livello di programmazione, registrate un Servlet Sling in ascolto di una `sitemap.xml` chiamata. Il servlet può quindi utilizzare la risorsa fornita tramite l&#39;API servlet per esaminare la pagina corrente e i relativi elementi secondari, producendo codice XML. Il codice XML verrà quindi memorizzato nella cache del dispatcher. A questa posizione deve fare riferimento nella proprietà sitemap del `robots.txt` file. Inoltre, sarà necessario implementare una regola di scaricamento personalizzata per fare in modo che il file venga scaricato ogni volta che viene attivata una nuova pagina.

>[!NOTE]
>
>È possibile registrare un Servlet Sling per ascoltare il selettore `sitemap` con l&#39;estensione `xml`. Questo causerà l’elaborazione della richiesta da parte del servlet ogni volta che viene richiesto un URL che termina in:
>    `/<path-to>/page.sitemap.xml`
Potete quindi ottenere la risorsa richiesta dalla richiesta e generare un sitemap da quel punto nella struttura del contenuto utilizzando le API JCR.
Il vantaggio di un approccio come questo è rappresentato dal fatto che più siti vengono serviti dalla stessa istanza. Una richiesta per `/content/siteA.sitemap.xml` generare un sitemap per `siteA` mentre una richiesta per `/content/siteB.sitemap.xml` creare un sitemap per `siteB` senza la necessità di scrivere codice aggiuntivo.

### Creazione di reindirizzamenti 301 per gli URL legacy {#creating-redirects-for-legacy-urls}

Quando si avvia un sito con una nuova struttura, è importante implementare e testare i reindirizzamenti 301 nel server Apache HTTP per due motivi:

* Gli URL precedenti hanno generato nel tempo un valore SEO predefinito. Implementando un reindirizzamento, il motore di ricerca può applicare questo valore al nuovo URL.
* Gli utenti del sito potrebbero aver creato segnalibri per queste pagine. Implementando i reindirizzamenti, potete essere certi di indirizzare l&#39;utente alla pagina del nuovo sito che corrisponde più da vicino a dove stava cercando di arrivare sul vecchio sito.

Accertatevi di controllare la sezione delle risorse aggiuntive che segue per istruzioni sull&#39;implementazione dei reindirizzamenti 301, nonché uno strumento per verificare che i reindirizzamenti funzionino come previsto.

## Additional Resources {#additional-resources}

Per ulteriori informazioni, consulta le seguenti risorse aggiuntive:

* [Mapping delle risorse](/help/sites-deploying/resource-mapping.md)
* [https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url](https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url)
* [https://moz.com/blog/15-seo-best-practices-for-structuring-urls](https://moz.com/blog/15-seo-best-practices-for-structuring-urls)
* [https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/](https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/)
* [https://sling.apache.org/documentation/the-sling-engine/servlets.html](https://sling.apache.org/documentation/the-sling-engine/servlets.html)
* [https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
* [https://httpd.apache.org/docs/current/mod/mod_rewrite.html](https://httpd.apache.org/docs/current/mod/mod_rewrite.html)
* [https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps](https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps)
* [https://www.robotstxt.org/robotstxt.html](https://www.robotstxt.org/robotstxt.html)
* [https://www.internetmarketingninjas.com/blog/search-engine-optimization/301-redirects/](https://www.internetmarketingninjas.com/blog/search-engine-optimization/301-redirects/)
* [https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester)
* [https://adobe-consulting-services.github.io/](https://adobe-consulting-services.github.io/)

