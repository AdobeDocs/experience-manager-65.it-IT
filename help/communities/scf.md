---
title: Quadro componente sociale
seo-title: Quadro componente sociale
description: Il quadro della componente sociale (SCF) semplifica il processo di configurazione, personalizzazione ed estensione dei componenti Community
seo-description: Il quadro della componente sociale (SCF) semplifica il processo di configurazione, personalizzazione ed estensione dei componenti Community
uuid: 23b4418d-b91c-46fc-bf42-1154ef79fe5a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d7b5b5e3-2d84-4a6b-bcc2-d490882ff3ed
translation-type: tm+mt
source-git-commit: 6ab91667ad668abf80ccf1710966169b3a187928
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 0%

---


# Quadro componente sociale {#social-component-framework}

Il social component framework (SCF) semplifica il processo di configurazione, personalizzazione ed estensione dei componenti Community sia sul lato server che sul lato client.

I vantaggi del quadro:

* **Funzionale**: Semplicità di integrazione con poca o nessuna personalizzazione per l&#39;80% dei casi di utilizzo.
* **Skinnable**: Uso coerente degli attributi HTML per lo stile CSS.
* **Estensibile**: L&#39;implementazione dei componenti è orientata agli oggetti e si basa sulla logica aziendale, per aggiungere facilmente accessi aziendali incrementali sul server.
* **Flessibilità**: Semplici modelli javascript senza logica, facilmente sovrapposti e personalizzati.
* **Accessibile**: L&#39;API HTTP supporta la pubblicazione da qualsiasi client, incluse le app mobili.
* **Portatile**: Integrare/incorporare in qualsiasi pagina Web basata su qualsiasi tecnologia.

Esplora un’istanza di creazione o pubblicazione utilizzando la guida [interattiva sui componenti](components-guide.md)community.

## Panoramica {#overview}

In SCF, un componente è composto da un POJO SocialComponent, un Modello JS Handlebars (per il rendering del componente) e CSS (per lo stile del componente).

Un modello JS Handlebars può estendere i componenti JS model/view per gestire l&#39;interazione dell&#39;utente con il componente sul client.

Se un componente deve supportare la modifica dei dati, l&#39;implementazione dell&#39;API SocialComponent può essere scritta per supportare la modifica/il salvataggio di dati simili a oggetti modello/dati nelle applicazioni Web tradizionali. Inoltre, è possibile aggiungere operazioni (controller) e un servizio operativo per gestire le richieste di operazioni, eseguire business logic e richiamare le API negli oggetti modello/dati.

L&#39;API SocialComponent può essere estesa per fornire i dati richiesti da un client per un livello di visualizzazione o un client HTTP.

### Rendering delle pagine per il client {#how-pages-are-rendered-for-client}

![rendering scf-pagina](assets/scf-overview.png)

### Personalizzazione ed estensione dei componenti {#component-customization-and-extension}

Per personalizzare o estendere i componenti, potete scrivere solo le sovrapposizioni e le estensioni nella directory /apps per semplificare il processo di aggiornamento alle release future.

* Per l&#39;interfaccia:
   * Solo il [CSS deve essere modificato](client-customize.md#skinning-css).
* Per aspetto:
   * Modificate i modelli JS e CSS.
* Per Look, Feel e UX:
   * Modificate il modello JS, CSS e [estendete/ignorate Javascript](client-customize.md#extending-javascript).
* Per modificare le informazioni disponibili per il modello JS o per l&#39;endpoint GET:
   * Estende il [SocialComponent](server-customize.md#socialcomponent-interface).
* Per aggiungere l&#39;elaborazione personalizzata durante le operazioni:
   * Scrivere un [OperationExtension](server-customize.md#operationextension-class).
* Per aggiungere una nuova operazione personalizzata:
   * Creare una nuova operazione [Sling Post](server-customize.md#postoperation-class).
   * Utilizzare [OperationServices](server-customize.md#operationservice-class) esistente come necessario.
   * Aggiungete il codice JavaScript per richiamare l&#39;operazione dal lato client in base alle esigenze.

## Framework lato server {#server-side-framework}

Il framework fornisce alle API l&#39;accesso alle funzionalità sul server e il supporto dell&#39;interazione tra client e server.

### API Java {#java-apis}

Le API Java forniscono classi e interfacce astratte che possono essere facilmente ereditate o sottoclassificate.

Le classi principali sono descritte nella pagina Personalizzazione [lato](server-customize.md) server.

Per informazioni sull&#39;utilizzo di UGC, visitare [Panoramica](srp.md) sui provider di risorse di storage.

### HTTP API {#http-api}

L&#39;API HTTP supporta la facilità di personalizzazione e la scelta delle piattaforme client per le app PhoneGap, le app native e altre integrazioni e mashup. Inoltre, l&#39;API HTTP consente a un sito community di essere eseguito come servizio senza client, in modo che i componenti framework possano essere integrati in qualsiasi pagina Web creata su qualsiasi tecnologia.

### API HTTP - Richieste di GET {#http-api-get-requests}

Per ogni componente Social, il framework fornisce un endpoint API basato su HTTP. L&#39;accesso all&#39;endpoint viene effettuato inviando una richiesta di GET alla risorsa con un selettore + estensione &#39;.social.json&#39;. Utilizzando Sling, la richiesta viene trasmessa al `DefaultSocialGetServlet`.

**`DefaultSocialGetServlet`**

1. Trasmette la risorsa (resourceType) all&#39; `SocialComponentFactoryManager` utente e riceve un SocialComponentFactory in grado di selezionare una risorsa `SocialComponent` che rappresenta la risorsa.

1. Richiama la fabbrica e riceve una `SocialComponent` capacità di gestione della risorsa e della richiesta.
1. Richiama il `SocialComponent`, che elabora la richiesta e restituisce una rappresentazione JSON dei risultati.
1. Restituisce la risposta JSON al client.

**`GET Request`**

Un servlet di GET predefinito ascolta le richieste .social.json alle quali SocialComponent risponde con JSON personalizzabile.

![scf-framework](assets/scf-framework.png)

### API HTTP - Richieste POST {#http-api-post-requests}

Oltre alle operazioni di GET (lettura), il framework definisce un pattern di endpoint per abilitare altre operazioni su un componente, tra cui Crea, Aggiorna ed Elimina. Tali endpoint sono API HTTP che accettano l&#39;input e rispondono con codici di stato HTTP o con un oggetto di risposta JSON.

Questo modello di endpoint framework rende le operazioni CUD estensibili, riutilizzabili e testabili.

**`POST Request`**

Esiste un&#39;operazione Sling POST:operation per ogni operazione SocialComponent. Il codice business logic e di manutenzione di ciascuna operazione è incluso in un servizio OperationService accessibile tramite l&#39;API HTTP o da un&#39;altra ubicazione come servizio OSGi. Sono disponibili blocchi che supportano le estensioni di funzionamento collegabili per le azioni prima/dopo.

![scf-post-richiesta](assets/scf-post-request.png)

### Provider di risorse di storage (SRP) {#storage-resource-provider-srp}

Per informazioni sulla gestione di UGC memorizzati nell&#39;archivio [dei contenuti della](working-with-srp.md)community, vedi:

* [Panoramica](srp.md) del provider delle risorse di storage - Introduzione e panoramica sull&#39;utilizzo dell&#39;archivio.
* [SRP e UGC Essentials](srp-and-ugc.md) - Metodi e esempi di utilità API SRP.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - Linee guida per la codifica.

### Personalizzazioni lato server {#server-side-customizations}

Per informazioni su come personalizzare la logica e il comportamento di un componente Community sul lato server, visita Personalizzazioni lato [server](server-customize.md) .

## Handlebars JS Template Language {#handlebars-js-templating-language}

Una delle modifiche più evidenti nel nuovo framework è l&#39;utilizzo del linguaggio HBS ( [Handlebars JS Template Language)](https://www.handlebarsjs.com/), una popolare tecnologia open-source per il rendering server-client.

Gli script HBS sono semplici, senza logica, compilati sia sul server che sul client, sono facili da sovrapporre e personalizzare e si legano naturalmente con l&#39;UX client, perché HBS supporta il rendering lato client.

Il framework fornisce diversi [strumenti](handlebars-helpers.md) Handlebars utili per lo sviluppo di SocialComponents.

Sul server, quando Sling risolve una richiesta di GET, identifica lo script che verrà utilizzato per rispondere alla richiesta. Se lo script è un modello HBS (.hbs), Sling delegherà la richiesta al motore Handlebars. Il motore handlebars otterrà il SocialComponent dalla SocialComponentFactory appropriata, creerà un contesto ed eseguirà il rendering del codice HTML.

### Nessuna limitazione di accesso {#no-access-restriction}

I file modello handlebars (HBS) (.hbs) sono analoghi ai file modello .jsp e .html, ma possono essere utilizzati per il rendering sia nel browser client che nel server. Pertanto, un browser client che richiede un modello lato client riceverà un file .hbs dal server.

Ciò richiede che tutti i modelli HBS nel percorso di ricerca sling (qualsiasi file .hbs in /libs/ o /apps) possano essere recuperati da qualsiasi utente dall&#39;autore o dalla pubblicazione.

L&#39;accesso HTTP ai file .hbs potrebbe non essere vietato.

### Aggiunta o inclusione di un componente Community {#add-or-include-a-communities-component}

La maggior parte dei componenti Community deve essere *aggiunta* come risorsa indirizzabile Sling. Alcuni componenti Community possono essere *inclusi* in un modello come risorsa non esistente per consentire l&#39;inclusione dinamica e la personalizzazione della posizione in cui scrivere il contenuto generato dall&#39;utente (UGC).

In entrambi i casi, devono essere presenti anche le librerie [client](clientlibs.md) richieste per il componente.

**Aggiunta di un componente**

L’aggiunta di un componente fa riferimento al processo di aggiunta di un’istanza di una risorsa (componente), ad esempio quando viene trascinata dal browser Componenti (barra laterale) su una pagina in modalità di modifica dell’autore.

Il risultato è un nodo figlio JCR sotto un nodo par, che è indirizzabile Sling.

**Includi un componente**

L’inclusione di un componente fa riferimento al processo di aggiunta di un riferimento a una risorsa [](srp.md#for-non-existing-resources-ners) &quot;non esistente&quot; (nessun nodo JCR) all’interno del modello, ad esempio l’uso di un linguaggio di script.

A partire da AEM 6.1, quando un componente viene incluso dinamicamente invece che aggiunto, è possibile modificare le proprietà del componente nel modo *design *authoring.

È possibile includere in modo dinamico solo alcuni dei  componenti AEM Communities. Sono:

* [Commenti](essentials-comments.md)
* [Valutazione](rating-basics.md)
* [Recensioni](reviews-basics.md)
* [Votazione](essentials-voting.md)

La Guida [ai componenti](components-guide.md) della community consente di passare dall’aggiunta all’inclusione di componenti inclusi.

**Quando si utilizza il linguaggio di modellazione Handlebars** , la risorsa non esistente viene inclusa utilizzando l&#39;helper [](handlebars-helpers.md#include) include specificando il relativo resourceType:

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**Quando si utilizza JSP**, una risorsa viene inclusa utilizzando il tag [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>Per aggiungere un componente a una pagina in modo dinamico, invece di aggiungerlo o includerlo in un modello, vedere [Bendeloading](sideloading.md)per componenti.


### Helper manubrio {#handlebars-helpers}

Per un elenco e una descrizione degli assistenti personalizzati disponibili in SCF, vedere [Helpers](handlebars-helpers.md) .

## Framework lato client {#client-side-framework}

### Framework Javascript con vista modello {#model-view-javascript-framework}

Il framework include un&#39;estensione di [Backbone.js](https://www.backbonejs.org/), un framework JavaScript con vista modello, per facilitare lo sviluppo di componenti interattivi avanzati. La natura orientata agli oggetti supporta un framework estensibile/riutilizzabile. La comunicazione tra client e server viene semplificata tramite l&#39;API HTTP.

Il framework utilizza i modelli Handlebars lato server per eseguire il rendering dei componenti per il client. I modelli si basano sulle risposte JSON generate dall&#39;API HTTP. Le viste si legano al codice HTML generato dai modelli Handlebars e forniscono interattività.

### Convenzioni CSS {#css-conventions}

Di seguito sono illustrate le convenzioni consigliate per definire e utilizzare le classi CSS:

* Utilizzate nomi di selettore di classe CSS chiaramente associati al nome ed evitate nomi generici quali &quot;heading&quot;, &quot;image&quot;, ecc.
* Definite stili di selettore di classe specifici in modo che i fogli di stile CSS funzionino correttamente con altri elementi e stili sulla pagina. Esempio: `.social-forum .topic-list .li { color: blue; }`
* Separate le classi CSS per lo stile dalle classi CSS per gli UX guidate da JavaScript.

### Personalizzazioni lato client {#client-side-customizations}

Per personalizzare l’aspetto e il comportamento di un componente Community sul lato client, fate riferimento a Personalizzazioni lato [client](client-customize.md), che include informazioni su:

* [Sovrapposizioni](client-customize.md#overlays)
* [Estensioni](client-customize.md#extensions)
* [Tag HTML](client-customize.md#htmlmarkup)
* [Skin CSS](client-customize.md#skinning-css)
* [Estensione di Javascript](client-customize.md#extending-javascript)
* [Clientlibs per SCF](client-customize.md#clientlibs-for-scf)

## Funzionalità e componenti di base {#feature-and-component-essentials}

Le informazioni essenziali per gli sviluppatori sono descritte nella sezione [Feature and Component Essentials (Funzioni e componenti essenziali](essentials.md) ).

Ulteriori informazioni sugli sviluppatori sono disponibili nella sezione [Coding Guidelines (Linee guida](code-guide.md) per la codifica).

## Risoluzione dei problemi {#troubleshooting}

I problemi comuni e i problemi noti sono descritti nella sezione [Risoluzione](troubleshooting.md) dei problemi.

