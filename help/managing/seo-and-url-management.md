---
title: Best practice per la gestione di SEO e URL
description: Scopri le best practice e le raccomandazioni SEO per l’implementazione di AEM.
topic-tags: managing
content-type: reference
docset: aem65
exl-id: b138f6d1-0870-4071-b96e-4a759ad9a76e
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Developer,Leader
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: ht
source-wordcount: '3522'
ht-degree: 100%

---

# Best practice per la gestione di SEO e URL{#seo-and-url-management-best-practices}

L’ottimizzazione SEO (Search Engine Optimization) è diventata un aspetto cruciale per molti marketer. Di conseguenza, i problemi relativi alla SEO devono essere affrontati in molti Progetti AEM.

In questo documento vengono innanzitutto descritte alcune [best practice SEO](#seo-best-practices) e alcuni consigli relativi all’implementazione di AEM. Vengono quindi approfonditi alcuni dei [passaggi di implementazione più complessi](#aem-configurations) illustrati nella prima sezione.

## Best practice per l’ottimizzazione SEO {#seo-best-practices}

Questa sezione descrive alcune best practice generali relative all’ottimizzazione SEO (Search Engine Optimization).

### URL {#urls}

Negli URL sono presenti alcune best practice accettate.

Durante la valutazione degli URL nel progetto AEM, prendi in considerazione le seguenti domande:

“Se un utente ha visualizzato questo URL e nessuno dei contenuti della pagina, potrebbe descriverla?”

Se la risposta è affermativa, è probabile che l’URL funzioni correttamente per un motore di ricerca.

Ecco alcuni suggerimenti di carattere generale su come creare URL per l’ottimizzazione SEO (Search Engine Optimization):

* Separa le parole con un trattino.

   * Usa i trattini (-) come separatori nei nomi delle pagine.
   * Evita di usare la notazione camel, caratteri di sottolineatura e spazi.

* Se possibile, evita l’uso di parametri di query. In caso di necessità, limitali a un massimo di due.

   * Utilizza la struttura di directory per indicare l’architettura delle informazioni, se disponibile.
   * Se non puoi utilizzare una struttura di directory, utilizza i selettori Sling invece delle stringhe di query nell’URL. Oltre a fornire il valore SEO, i selettori Sling consentono anche di rendere le pagine memorizzabili nella cache per Dispatcher.

* Un URL chiaro e leggibile è sempre meglio. La presenza di parole chiave nell’URL ne aumenta il valore.

   * Se utilizzi selettori in una pagina, scegli quelli che forniscono valori semantici.
   * Se un utente non riesce a interpretare l’URL, non può farlo nemmeno un motore di ricerca.
   * Ad esempio:
     `mybrand.com/products/product-detail.product-category.product-name.html`
è da preferirsi a `mybrand.com/products/product-detail.1234.html`

* Se possibile, evita i sottodomini perché i motori di ricerca li considereranno come entità diverse, frammentando il valore SEO del sito.

   * Utilizza invece percorsi secondari di primo livello. Ad esempio, usa `www.mybrand.com/es/home.html` invece di `es.mybrand.com/home.html`.

   * Pianifica la gerarchia dei contenuti in modo che corrisponda all’ordine in cui verranno presentati, in base a questa linea guida.

* Le parole chiave negli URL perdono efficacia se si trovano in URL lunghi e se non sono posizionate all’inizio. In altre parole, scegli URL brevi.

   * Utilizza le tecniche e le funzioni di abbreviazione degli URL fornite da AEM per rimuovere gli elementi superflui.
   * Ad esempio, `mybrand.com/en/myPage.html` è da preferirsi a `mybrand.com/content/my-brand/en/myPage.html`.

* Utilizza URL canonici.

   * Quando un URL può essere gestito da percorsi diversi o con parametri o selettori diversi, assicurati di usare un tag `rel=canonical` nella pagina.

   * Includi URL canonici nel codice del modello AEM.

* Se possibile, fai in modo che l’URL corrisponda al titolo della pagina.

   * Invita gli autori dei contenuti a seguire questa pratica.

* Non richiedere il rispetto della distinzione tra maiuscole/minuscole nelle richieste URL.

   * Configura il Dispatcher in modo da riscrivere in lettere minuscole tutte le richieste in entrata.
   * Chiedi agli autori di contenuti di creare tutte le pagine utilizzando solo lettere minuscole.

* Assicurati che ogni pagina sia gestita da un solo protocollo.

   * A volte i siti vengono gestiti tramite `http` fino a quando l’utente non raggiunge una pagina contenente, ad esempio, un modulo di pagamento o di accesso, che viene gestito tramite `https`. Quando il collegamento viene effettuato da questa pagina, se l’utente può tornare alle `http` pagine e accedervi tramite questi `https`, il motore di ricerca ne tiene traccia come se fossero due pagine separate.

   * Google attualmente preferisce le pagine `https` a quelle `http`. Contribuiscono a semplificare la gestione dell’intero sito tramite `https`.

### Configurazione del server {#server-configuration}

Dal punto di vista della configurazione del server, puoi adottare le seguenti misure per garantire che venga effettuata la ricerca per indicizzazione solo del contenuto corretto:

* Utilizza un file `robots.txt` per bloccare la ricerca per indicizzazione di qualsiasi contenuto che non deve essere indicizzato.

   * Blocca **tutte** le operazioni di ricerca per indicizzazione negli ambienti di test.

* Quando lanci un nuovo sito con URL aggiornati, implementa i reindirizzamenti 301 per non perdere il tuo ranking SEO esistente.
* Includi un favicon per il tuo sito.
* Per permettere ai motori di ricerca di indicizzare più facilmente i contenuti, implementa una mappa del sito XML. Assicurati di includere una mappa del sito per dispositivi mobili per i siti mobili e/o dinamici.

## Configurazioni AEM {#aem-configurations}

Questa sezione descrive i passaggi di implementazione necessari per configurare AEM con i seguenti consigli SEO.

### Utilizzo dei selettori Sling {#using-sling-selectors}

In precedenza, per la creazione di un’applicazione web aziendale si usavano in genere i parametri di query.

Negli ultimi anni, la tendenza è stata quella di rimuovere i parametri per migliorare la leggibilità degli URL. Su molte piattaforme, questo processo di rimozione comporta l’implementazione di reindirizzamenti sul server web o sulla rete per la consegna dei contenuti (CDN), ma Sling rende questa operazione semplice. I selettori Sling:

* Migliorano la leggibilità degli URL.
* Consentono di memorizzare le pagine nella cache di Dispatcher e migliorano la sicurezza.
* Consentono di gestire il contenuto direttamente, invece di avere un servlet generico per il recupero del contenuto. Ciò permette di sfruttare i vantaggi degli ACL da applicare all’archivio e ai filtri che applichi al Dispatcher.

#### Utilizzo dei selettori per i servlet {#using-selectors-for-servlets}

AEM offre due opzioni per la scrittura di servlet:

* Servlet **bin**
* Servlet **Sling**

Gli esempi seguenti illustrano come registrare i servlet conformi a questi modelli che consentono di sfruttare i vantaggi ottenuti utilizzando i servlet Sling.

#### Servlet Bin (un livello inferiore) {#bin-servlets-one-level-down}

I servlet **Bin** sono conformi al modello a cui molti sviluppatori sono abituati dalla programmazione J2EE. Il servlet viene registrato in un percorso specifico che, in AEM, si trova in genere in `/bin` e l’utente estrae i parametri dalla stringa di query.

L’annotazione SCR per questo tipo di servlet sarà simile alla seguente:

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

Estrai quindi i parametri dalla stringa di query tramite l’oggetto `SlingHttpServletRequest` incluso nel metodo `doGet`; ad esempio:

```
String myParam = req.getParameter("myParam");
```

L’URL risultante usato sarà simile al seguente:

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

Con questo approccio ci sono alcuni aspetti da considerare:

* L’URL stesso perde valore SEO. Gli utenti che accedono al sito, inclusi i motori di ricerca, non ricevono alcun valore semantico dall’URL, in quanto l’URL rappresenta un percorso programmatico e non la gerarchia dei contenuti.
* La presenza di parametri di query nell’URL impedisce a Dispatcher di memorizzare la risposta nella cache.
* Per proteggere questo servlet, è necessario implementare una logica di sicurezza personalizzata nel servlet.
* Il Dispatcher deve essere configurato (con attenzione) in modo da esporre `/bin/myApp/myServlet`. La semplice esposizione di `/bin` consentirebbe l’accesso a determinati servlet che non dovrebbero essere aperti ai visitatori del sito.

#### Servlet Sling (un livello inferiore) {#sling-servlets-one-level-down}

I servlet **Sling** permettono di registrare il servlet in modo opposto. Invece di gestire un servlet e specificare il contenuto di cui vuoi eseguire il rendering in base ai parametri della query, devi gestire il contenuto desiderato. Inoltre, specifica il servlet che deve eseguire il rendering del contenuto in base ai selettori Sling.

L’annotazione SCR per questo tipo di servlet sarà simile alla seguente:

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json", methods="GET")
```

In questo caso, la risorsa gestita dall’URL (un’istanza della risorsa `myPageType`) è accessibile automaticamente nel servlet. Per accedervi, chiama:

```
Resource myPage = req.getResource();
```

L’URL risultante usato sarà simile al seguente:

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

I vantaggi di questo approccio sono i seguenti:

* Puoi incorporare valore SEO (Search Engine Optimization), ottenuto dalla semantica presente nella gerarchia del sito e nel nome della pagina.
* Poiché non sono presenti parametri di query, il Dispatcher può memorizzare la risposta nella cache. Inoltre, eventuali aggiornamenti apportati alla pagina gestita annulleranno la validità della cache quando la pagina viene attivata.
* Tutti gli ACL applicati a `/content/my-brand/my-page` diventano effettivi quando un utente tenta di accedere a questo servlet.
* Il Dispatcher è già configurato per servire questo contenuto come funzione della gestione del sito web. Non è richiesta alcuna configurazione aggiuntiva.

### Riscrittura di URL {#url-rewriting}

In AEM, tutte le pagine web vengono archiviate in `/content/my-brand/my-content`. Anche se questa posizione è utile dal punto di vista della gestione dei dati dell’archivio, non corrisponde necessariamente alla modalità di visualizzazione del sito da parte della clientela. Inoltre, mantenere gli URL il più brevi possibile potrebbe entrare in conflitto con le linee guida SEO. È anche possibile che più siti web vengano gestiti dalla stessa istanza di AEM e da nomi di dominio diversi.

Questa sezione esamina le opzioni disponibili in AEM per gestire questi URL e presentarli agli utenti in modo più leggibile e compatibile con SEO.

#### Gli URL personalizzati {#vanity-urls}

Se un autore vuole che una pagina sia accessibile da una seconda posizione a scopo promozionale, potrebbe essere utile utilizzare gli URL personalizzati di AEM, definiti pagina per pagina. Per aggiungere un URL personalizzato a una pagina, passa alla pagina nella console **Sites** e modifica le proprietà della pagina. Nella parte inferiore della scheda **Base**, è disponibile una sezione in cui è possibile aggiungere URL personalizzati. Tieni presente che l’accesso alla pagina tramite più URL comporterà la frammentazione del valore SEO della pagina. Per evitare questo problema è quindi necessario aggiungere alla pagina un tag di URL canonico.

#### Nomi di pagina localizzati {#localized-page-names}

Può essere necessario visualizzare i nomi delle pagine localizzate agli utenti del contenuto tradotto. Ad esempio:

* L’URL visualizzato da un utente di lingua spagnola non dovrebbe essere:
  `www.mydomain.com/es/home.html`

* Ma sarebbe meglio che fosse:
  `www.mydomain.com/es/casa.html`.

Il problema correlato alla localizzazione del nome della pagina è che molti degli strumenti di localizzazione disponibili sulla piattaforma AEM dipendono dalla corrispondenza dei nomi delle pagine tra diverse lingue, per garantire la sincronizzazione del contenuto.

La proprietà `sling:alias` ti permette di risolverlo anche con Adobe. Puoi aggiungere `sling:alias` come proprietà a qualsiasi risorsa per consentire l’utilizzo di un nome di alias della risorsa. Nell’esempio precedente, avrai:

* Una pagina nel JCR in:
  `…/es/home`

* Una proprietà aggiunta a tale pagina:
  `sling:alias` = `casa`

Questo flusso permette agli strumenti di traduzione di AEM, come l’utilità di gestione di più siti, di continuare a mantenere una relazione tra:

* `/en/home`

* `/es/home`

Allo stesso tempo gli utenti finali potranno interagire con il nome della pagina nelle rispettive lingue native.

>[!NOTE]
>
>È possibile impostare la proprietà `sling:alias` utilizzando la [proprietà Alias durante la modifica delle proprietà della pagina](/help/sites-authoring/editing-page-properties.md#advanced).

#### /etc/map {#etc-map}

In un’installazione standard di AEM:

* per la configurazione OSGi
  **Apache Sling Resource Resolver Factory**
( `org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`)

* la proprietà
  **Mapping Location** (Posizione mappatura) ( `resource.resolver.map.location`)

* viene impostata sul valore predefinito `/etc/map`.

È possibile aggiungere definizioni di mappatura in questa posizione per mappare le richieste in entrata, riscrivere gli URL nelle pagine in AEM o eseguire entrambe le operazioni.

Per creare una mappatura, crea un nodo `sling:Mapping` in questa posizione in `/http` o `/https`. In base alle proprietà `sling:match` e `sling:internalRedirect` impostate su questo nodo, AEM reindirizzerà tutto il traffico dell’URL corrispondente al valore specificato nella proprietà `internalRedirect`.

Anche se questo è l’approccio illustrato nella documentazione ufficiale di AEM e Sling, il regolare supporto delle espressioni fornito da questa implementazione ha un ambito limitato rispetto alle opzioni disponibili utilizzando direttamente `SlingResourceResolver`. Inoltre, una tale implementazione delle mappature può causare problemi con l’annullamento della validità della cache del Dispatcher.

Ecco un esempio di scenario in cui si verifica questo problema:

1. Un utente visita il sito web e richiede `https://www.mydomain.com/my-page.html`
1. Il Dispatcher inoltra questa richiesta al server di pubblicazione.
1. Con `/etc/map`, il server di pubblicazione risolve la richiesta in `/content/my-brand/my-page` ed esegue il rendering della pagina.

1. Il Dispatcher memorizza nella cache la risposta in `/my-page.html` e restituisce la risposta all’utente.
1. Un autore di contenuti modifica e attiva la pagina.
1. L’agente di svuotamento del Dispatcher invia una richiesta di annullamento della validità per `/content/my-brand/my-page`**.** Poiché il Dispatcher non ha una pagina memorizzata nella cache in questo percorso, il contenuto precedente rimane memorizzato nella cache e non viene aggiornato.

Sono disponibili vari modi per configurare regole di eliminazione personalizzate che mappano l’URL più breve all’URL più lungo per consentire l’annullamento della validità della cache.

Esiste però anche una soluzione più semplice per gestire questo problema:

1. **Regole di SlingResourceResolver**

   Utilizzando la console web (ad esempio localhost:4502/system/console/configMgr), puoi configurare Sling Resource Resolver:

   * **Apache Sling Resource Resolver Factory**
     `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`.

   Adobe consiglia di creare le mappature necessarie per ridurre gli URL come espressioni regolari, quindi definire queste configurazioni in un nodo OsgiConfignode `config.publish`, incluso nella build.

   Invece di definire le mappature in `/etc/map`, puoi assegnarle direttamente alla proprietà **URL Mappings** (Mappature URL) ( `resource.resolver.mapping`):

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   In questo semplice esempio rimuoverai `/content/my-brand/` dall’inizio di tutti gli URL in cui è presente.

   Converte un URL:

   * da `/content/my-brand/my-page.html`
   * a semplicemente `/my-page.html`

   Questa conversione è in linea con la pratica consigliata di ridurre quanto più possibile la lunghezza degli URL.

1. **Mappatura dell’output degli URL nelle pagine**

   Dopo aver definito le mappature in Apache Sling Resource Resolver, utilizzale nei componenti per garantire che gli URL generati nelle pagine siano brevi e leggibili. Per eseguire questa gestione, puoi utilizzare la funzione di mappatura di `ResourceResolver`.

   Se, ad esempio, stai implementando un componente di navigazione personalizzato che elenca gli elementi secondari della pagina corrente, puoi utilizzare il metodo di mappatura nel modo seguente:

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### mod_rewrite di Apache HTTP Server {#apache-http-server-mod-rewrite}

Finora, hai implementato le mappature unitamente alla logica presente nei tuoi componenti per utilizzarle durante la creazione dell’output degli URL nelle pagine.

Non resta che definire come gestire questi URL abbreviati quando arrivano al Dispatcher ed è qui che entra in gioco `mod_rewrite`. Il principale vantaggio associato all’uso di `mod_rewrite` è che gli URL vengono mappati sulla relativa forma estesa *prima* di essere inviati al modulo del Dispatcher. Questo flusso significa che il Dispatcher richiederà l’URL esteso al server di pubblicazione e lo memorizzerà nella cache di conseguenza. Pertanto, qualsiasi richiesta di eliminazione del Dispatcher proveniente dal server di pubblicazione può annullare la validità di questo contenuto.

Per implementare queste regole, puoi aggiungere elementi `RewriteRule` nell’host virtuale della configurazione di Apache HTTP Server. Se vuoi espandere gli URL abbreviati dell’esempio precedente, puoi implementare una regola simile alla seguente:

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### Tag di URL canonici {#canonical-url-tags}

I tag URL canonici sono tag di collegamento inseriti nell’intestazione di un documento HTML che consentono di definire la modalità di gestione di una pagina nei motori di ricerca durante l’indicizzazione del contenuto. Questo approccio offre il vantaggio di garantire che una pagina o versioni diverse di essa vengano indicizzate allo stesso modo anche quando l’URL della pagina presenta differenze.

Se, ad esempio, un sito include una versione di una pagina adatta alla stampa, un motore di ricerca potrebbe indicizzarla come pagina diversa da quella della versione normale della stessa pagina. Il tag canonico indica al motore di ricerca che tali pagine sono uguali.

Esempi:

* `https://www.mydomain.com/my-brand/my-page.html`
* `https://www.mydomain.com/my-brand/my-page.print.html`

Per entrambi viene applicato il seguente tag all’intestazione della pagina:

```xml
<link rel="canonical" href="my-brand/my-page.html"/>
```

Il valore `href` può essere relativo o assoluto. Per determinare l’URL canonico per la pagina e generare questo tag, il codice deve essere incluso nel markup della pagina.

### Configurazione del Dispatcher per rimuovere la distinzione tra maiuscole/minuscole {#configuring-the-dispatcher-for-case-insensitivity}

Secondo la best practice, è consigliabile utilizzare solo lettere minuscole nei nomi di pagina. Se, però, non vuoi che un utente riceva un errore 404 quando accede al sito web utilizzando lettere maiuscole nell’URL, Adobe consiglia di aggiungere nella configurazione di Apache HTTP Server una regola di riscrittura per mappare tutti gli URL in arrivo utilizzando lettere minuscole. È inoltre necessario chiedere agli autori dei contenuti di utilizzare nomi contenenti solo lettere minuscole quando creano le pagine.

Per configurare Apache in modo che per tutto il traffico in entrata vengano utilizzate lettere minuscole, aggiungi quanto segue alla configurazione di `vhost`:

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

Aggiungi inoltre quanto segue nella parte iniziale del file `htaccess`:

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### Implementazione di robots.txt per proteggere gli ambienti di sviluppo {#implementing-robots-txt-to-protect-development-environments}

I motori di ricerca *devono* verificare la presenza di un file `robots.txt` nella directory principale del sito prima di eseguire la ricerca per l’indicizzazione del sito. Mentre i principali motori di ricerca come Google, Yahoo o Bing rispettano questo file, alcuni motori di ricerca di altri Paesi no.

Il modo più semplice per bloccare l’accesso all’intero sito consiste nell’inserire nella directory principale del sito un file denominato `robots.txt` con il seguente contenuto:

```xml
User-agent: *
Disallow: /
```

In alternativa, in un ambiente live, puoi scegliere di non consentire l’indicizzazione di determinati percorsi.

Avvertiamo però che posizionando il file `robots.txt` nella directory principale del sito, le richieste di svuotamento di Dispatcher potrebbero cancellare questo file. Inoltre, è probabile che le mappature URL posizionino la directory principale del sito in un punto diverso da `DOCROOT` come definito nella configurazione di Apache HTTP Server. Per questo motivo, questo file viene in genere inserito nell’istanza di authoring nella directory principale del sito e replicato nell’istanza di pubblicazione.

### Creazione di una mappa del sito XML in AEM {#building-an-xml-sitemap-on-aem}

I crawler utilizzano le mappe del sito XML per comprendere meglio la struttura dei siti web. Anche se non è detto che la creazione di una mappa del sito si traduca in un miglioramento dei ranking SEO, si tratta di una best practice comunemente accettata. Puoi gestire manualmente un file XML sul server web da utilizzare come mappa del sito. Tuttavia, Adobe consiglia di generare la mappa del sito a livello di programmazione, in modo che, quando gli autori creano contenuti, le modifiche apportate vengano applicate automaticamente alla mappa del sito.

AEM utilizza il [modulo Sitemap di Apache Sling](https://github.com/apache/sling-org-apache-sling-sitemap) per generare mappe del sito XML. Questo modulo fornisce un’ampia gamma di opzioni che consentono agli sviluppatori e agli editor di mantenere aggiornata la mappa del sito XML.

>[!NOTE]
>
>Disponibile come funzione prodotto a partire dalla versione 6.5.11.0 di Adobe Experience Manager.
> 
>Per le versioni precedenti, puoi registrare autonomamente un servlet Sling per ascoltare una chiamata `sitemap.xml`. Utilizza la risorsa fornita tramite l’API servlet per cercare la pagina corrente e i relativi discendenti e generare un file `sitemap.xml`.

Il modulo Sling Sitemap di Apache distingue tra una mappa del sito di livello superiore e una mappa del sito nidificata, entrambe generate per tutte le risorse per le quali la proprietà `sling:sitemapRoot` è impostata su `true`. In generale, le mappe del sito vengono sottoposte a rendering utilizzando i selettori nel percorso della mappa del sito di primo livello della struttura, che è la risorsa senza altri predecessori nella directory principale della mappa del sito. La directory principale della mappa del sito di primo livello espone anche l’indice della mappa del sito, che solitamente viene configurata da proprietario del sito nel portale di configurazione del motore di ricerca oppure aggiunta al file `robots.txt` del sito.

Ad esempio, considera un sito in cui la directory principale della mappa del sito di livello superiore è `my-page` e la directory principale di una mappa del sito nidificata è `my-page/news`, per generare una mappa del sito dedicata per le pagine della sottostruttura “news”. Gli url pertinenti risultanti sarebbero

* `https://www.mydomain.com/my-brand/my-page.sitemap-index.xml`
* `https://www.mydomain.com/my-brand/my-page.sitemap.xml`
* `https://www.mydomain.com/my-brand/my-page.sitemap.news-sitemap.html`

>[!NOTE]
>
>I selettori `sitemap` e `sitemap-index` possono interferire con le implementazioni personalizzate. Se non desideri utilizzare la funzione del prodotto, configura il tuo servlet che serve questi selettori con un `service.ranking` superiore a 0.

Nella configurazione predefinita, la finestra di dialogo Proprietà pagina consente di contrassegnare una pagina come radice di una sitemap e quindi, come descritto in precedenza, di generare una sitemap di se stessa e dei suoi discendenti. Questo comportamento è implementato dalle implementazioni dell’interfaccia `SitemapGenerator` e può essere esteso aggiungendo implementazioni alternative. Tuttavia, dato che la frequenza con cui rigenerare sitemap XML dipende dai flussi di lavoro e dai carichi di lavoro per l’authoring dei contenuti, il prodotto non viene fornito con alcuna configurazione `SitemapScheduler`. Come tale, rende la funzione effettivamente opt-in.

Per abilitare il processo in background che genera sitemap XML, `SitemapScheduler` deve essere configurato. Per farlo, crea una configurazione OSGI per il PID `org.apache.sling.sitemap.impl.SitemapScheduler`. Espressione di pianificazione `0 0 0 * * ?` può essere utilizzato come punto di partenza per rigenerare tutte le sitemap XML una volta al giorno a mezzanotte.

![Sitemap Apache Sling - Pianificazione](assets/sling-sitemap-scheduler.png)

Il processo di generazione della mappa del sito può essere eseguito su istanze di livello sia di authoring sia di pubblicazione. Nella maggior parte dei casi, è consigliabile eseguire la generazione sulle istanze del livello di pubblicazione, in quanto gli URL canonici corretti possono essere generati solo lì (a causa delle regole di mappatura risorse Sling comunemente presenti solo sulle istanze del livello di pubblicazione). Tuttavia, è possibile collegare un’implementazione personalizzata del meccanismo di esternalizzazione utilizzato per generare gli URL canonici implementando l’interfaccia [SitemapLinkExternalizer](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/sitemap/externalizer/SitemapLinkExternalizer.html). Se un’implementazione personalizzata è in grado di generare gli URL canonici di una mappa del sito sulle istanze del livello di authoring, `SitemapScheduler` può essere configurato per la modalità di esecuzione di authoring. Inoltre, il carico di lavoro di generazione della mappa del sito XML può essere distribuito tra le istanze del cluster del servizio di authoring. In questo scenario, occorre prestare particolare attenzione alla gestione di contenuti non ancora pubblicati, modificati o visibili solo a un gruppo ristretto di utenti.

AEM Sites contiene un’implementazione predefinita di un `SitemapGenerator` che attraversa una struttura ad albero di pagine per generare una sitemap. È preconfigurato per generare solo gli URL canonici di un sito e qualsiasi alternativa linguistica, se disponibile. Può anche essere configurato in modo da includere l’ultima data modificata di una pagina, se necessario. Per far questo, abilita l’opzione _Aggiungi ultima modificata_ di _Adobe AEM SEO - Configurazione del generatore della mappa del sito nella struttura ad albero della pagina_ e seleziona _Ultima origine modificata_. Quando vengono generate le mappe del sito sul livello di pubblicazione, si consiglia di utilizzare la data `cq:lastModified`.

![Adobe AEM SEO - Configurazione del generatore di sitemap nella struttura ad albero della pagina](assets/sling-sitemap-pagetreegenerator.png)

Per limitare il contenuto di una sitemap, è possibile implementare le seguenti interfacce di servizio quando necessario:

* [SitemapPageFilter](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/sitemap/SitemapPageFilter.html) può essere implementato per nascondere le pagine da sitemap XML generate dal generatore di sitemap specifico di AEM Sites
* [SitemapProductFilter](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/sitemap/SitemapProductFilter.html) o [SitemapCategoryFilter](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/sitemap/SitemapCategoryFilter.html) può essere implementato per filtrare prodotti o categorie da sitemap XML generati dai generatori di sitemap specifici [Framework di integrazione Commerce](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/home.html?lang=it)

Se le implementazioni predefinite non funzionano su un particolare caso d’uso o se i punti di estensione non sono abbastanza flessibili, implementa un `SitemapGenerator` personalizzato per assumere il controllo completo del contenuto di una mappa del sito generata. Nell’esempio seguente viene utilizzata la logica di implementazione predefinita per AEM Sites. Utilizza [ResourceTreeSitemapGenerator](https://javadoc.io/doc/org.apache.sling/org.apache.sling.sitemap/latest/org/apache/sling/sitemap/spi/generator/ResourceTreeSitemapGenerator.html) come punto iniziale per scorrere la struttura delle pagine:

```
import java.util.Optional;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.sitemap.SitemapException;
import org.apache.sling.sitemap.builder.Sitemap;
import org.apache.sling.sitemap.builder.Url;
import org.apache.sling.sitemap.spi.common.SitemapLinkExternalizer;
import org.apache.sling.sitemap.spi.generator.ResourceTreeSitemapGenerator;
import org.apache.sling.sitemap.spi.generator.SitemapGenerator;
import org.jetbrains.annotations.NotNull;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.aem.wcm.seo.sitemap.PageTreeSitemapGenerator;
import com.day.cq.wcm.api.Page;

@Component(
    service = SitemapGenerator.class,
    property = { "service.ranking:Integer=20" }
)
public class SitemapGeneratorImpl extends ResourceTreeSitemapGenerator {

    private static final Logger LOG = LoggerFactory.getLogger(SitemapGeneratorImpl.class);

    @Reference
    private SitemapLinkExternalizer externalizer;
    @Reference
    private PageTreeSitemapGenerator defaultGenerator;

    @Override
    protected void addResource(@NotNull String name, @NotNull Sitemap sitemap, Resource resource) throws SitemapException {
        Page page = resource.adaptTo(Page.class);
        if (page == null) {
            LOG.debug("Skipping resource at {}: not a page", resource.getPath());
            return;
        }
        String location = externalizer.externalize(resource);
        Url url = sitemap.addUrl(location + ".html");
        // add any additional content to the Url like lastmod, change frequency, and so on
    }

    @Override
    protected final boolean shouldFollow(@NotNull Resource resource) {
        return super.shouldFollow(resource)
            && Optional.ofNullable(resource.adaptTo(Page.class)).map(this::shouldFollow).orElse(Boolean.TRUE);
    }

    private boolean shouldFollow(Page page) {
        // add additional conditions to stop traversing some pages
        return !defaultGenerator.isProtected(page);
    }

    @Override
    protected final boolean shouldInclude(@NotNull Resource resource) {
        return super.shouldInclude(resource)
            && Optional.ofNullable(resource.adaptTo(Page.class)).map(this::shouldInclude).orElse(Boolean.FALSE);
    }

    private boolean shouldInclude(Page page) {
        // add additional conditions to stop including some pages
        return defaultGenerator.isPublished(page)
            && !defaultGenerator.isNoIndex(page)
            && !defaultGenerator.isRedirect(page)
            && !defaultGenerator.isProtected(page);
    }
}
```

Inoltre, la funzionalità implementata per le mappe del sito XML può essere utilizzata anche in casi d’uso diversi, ad esempio per aggiungere il collegamento canonico o le alternative di lingua nell’intestazione di una pagina. Per ulteriori informazioni, consulta l’interfaccia [SeoTags](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/SeoTags.html).

### Creazione di reindirizzamenti 301 per gli URL legacy {#creating-redirects-for-legacy-urls}

Quando si lancia un sito con una nuova struttura, è fondamentale implementare e testare i reindirizzamenti 301 in Apache HTTP Server per due motivi:

* Gli URL legacy hanno accumulato valore SEO nel tempo. Implementando un reindirizzamento, il motore di ricerca può applicare questo valore al nuovo URL.
* Gli utenti del sito potrebbero aver creato segnalibri per queste pagine. Grazie ai reindirizzamenti, gli utenti verranno reindirizzati alla pagina del nuovo sito che corrisponde maggiormente alla pagina a cui erano interessati nel vecchio sito.

Consulta la sezione seguente, dove troverai risorse aggiuntive con istruzioni sull’implementazione dei reindirizzamenti 301, nonché uno strumento per verificare che i reindirizzamenti funzionino come previsto.

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, consulta le seguenti risorse aggiuntive:

* [Mappatura delle risorse](/help/sites-deploying/resource-mapping.md)
* [https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url](https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url)
* [https://moz.com/blog/15-seo-best-practices-for-structuring-urls](https://moz.com/blog/15-seo-best-practices-for-structuring-urls)
* [https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/](https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/)
* [https://sling.apache.org/documentation/the-sling-engine/servlets.html](https://sling.apache.org/documentation/the-sling-engine/servlets.html)
* [https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
* [https://httpd.apache.org/docs/current/mod/mod_rewrite.html](https://httpd.apache.org/docs/current/mod/mod_rewrite.html)
* [https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps](https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps)
* [https://www.robotstxt.org/robotstxt.html](https://www.robotstxt.org/robotstxt.html)
* [https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester)
* [https://adobe-consulting-services.github.io/](https://adobe-consulting-services.github.io/)
