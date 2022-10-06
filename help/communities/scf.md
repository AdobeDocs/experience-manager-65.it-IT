---
title: Quadro dei componenti sociali
seo-title: Social Component Framework
description: Il quadro della componente sociale (SCF) semplifica il processo di configurazione, personalizzazione ed estensione dei componenti di Communities
seo-description: The social component framework (SCF) simplifies the process of configuring, customizing, and extending Communities components
uuid: 23b4418d-b91c-46fc-bf42-1154ef79fe5a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d7b5b5e3-2d84-4a6b-bcc2-d490882ff3ed
exl-id: 5ca58bc3-8505-4d91-9cd1-6b2e2671f1be
source-git-commit: 1d5cfff10735ea31dc0289b6909851b8717936eb
workflow-type: tm+mt
source-wordcount: '1483'
ht-degree: 0%

---

# Quadro dei componenti sociali {#social-component-framework}

Il framework dei componenti social (SCF) semplifica il processo di configurazione, personalizzazione ed estensione dei componenti di Communities sia sul lato server che sul lato client.

I vantaggi del quadro di riferimento:

* **Funzionale**: Semplicità di integrazione con poca o nessuna personalizzazione per l’80% dei casi d’uso.
* **Pelle**: Uso coerente degli attributi di HTML per lo stile CSS.
* **Estendibile**: L’implementazione dei componenti è orientata agli oggetti e si basa sulla logica di business: facile da aggiungere all’accesso incrementale di business sul server.
* **Flessibile**: Semplici modelli javascript senza logica, facilmente sovrapposti e personalizzati.
* **Accessibile**: L’API HTTP supporta la pubblicazione da qualsiasi client, incluse le app mobili.
* **Portatile**: Integra/incorpora in qualsiasi pagina web basata su qualsiasi tecnologia.

Esplora un’istanza di authoring o pubblicazione utilizzando l’interfaccia interattiva [Guida ai componenti della community](components-guide.md).

## Panoramica {#overview}

In SCF, un componente è composto da un POJO SocialComponent, un modello JS Handlebars (per eseguire il rendering del componente) e CSS (per personalizzare lo stile del componente).

Un modello JS Handlebars può estendere il modello/visualizzare i componenti JS per gestire l’interazione dell’utente con il componente sul client.

Se un componente deve supportare la modifica dei dati, l’implementazione dell’API SocialComponent può essere scritta per supportare la modifica/il salvataggio di dati simili agli oggetti modello/dati nelle applicazioni web tradizionali. È inoltre possibile aggiungere operazioni (controller) e un servizio operativo per gestire le richieste di operazioni, eseguire la logica di business e richiamare le API sugli oggetti modello/dati.

L’API SocialComponent può essere estesa per fornire i dati richiesti da un client per un livello di visualizzazione o un client HTTP.

### Rendering delle pagine per il client {#how-pages-are-rendered-for-client}

![rendering scf-page](assets/scf-overview.png)

### Personalizzazione ed estensione dei componenti {#component-customization-and-extension}

Per personalizzare o estendere i componenti, scrivi solo le sovrapposizioni e le estensioni nella directory /apps per semplificare il processo di aggiornamento alle versioni future.

* Per la skin:
   * Solo il [Modifica delle esigenze CSS](client-customize.md#skinning-css).
* Per look and Feel:
   * Modifica il modello JS e CSS.
* Per Look, Feel e UX:
   * Modificare il modello JS, CSS e [estendere/sostituire Javascript](client-customize.md#extending-javascript).
* Per modificare le informazioni disponibili sul modello JS o sull&#39;endpoint GET:
   * Estendi la [ComponenteSocial](server-customize.md#socialcomponent-interface).
* Per aggiungere un’elaborazione personalizzata durante le operazioni:
   * Scrivi un [OperationExtension](server-customize.md#operationextension-class).
* Per aggiungere una nuova operazione personalizzata:
   * Crea un nuovo [Funzionamento a post-Sling](server-customize.md#postoperation-class).
   * Usa esistente [OperationServices](server-customize.md#operationservice-class) se necessario.
   * Aggiungi il codice JavaScript per richiamare l&#39;operazione dal lato client in base alle esigenze.

## Framework lato server {#server-side-framework}

Il framework fornisce API per accedere alle funzionalità sul server e supportare l’interazione tra client e server.

### API Java {#java-apis}

Le API Java forniscono classi astratte e interfacce facilmente ereditate o sottoclassificate.

Le classi principali sono descritte nella sezione [Personalizzazione lato server](server-customize.md) pagina.

Visita [Panoramica del provider di risorse di storage](srp.md) per scoprire come utilizzare UGC.

### API HTTP {#http-api}

L’API HTTP supporta la facilità di personalizzazione e la scelta delle piattaforme client per le app PhoneGap, le app native e altre integrazioni e mashup. Inoltre, l&#39;API HTTP consente a un sito community di essere eseguito come servizio senza un client, in modo tale che i componenti del framework possano essere integrati in qualsiasi pagina web basata su qualsiasi tecnologia.

### API HTTP - Richieste GET {#http-api-get-requests}

Per ogni componente Social, il framework fornisce un endpoint API basato su HTTP. L’endpoint è accessibile inviando una richiesta GET alla risorsa con un selettore + estensione &#39;.social.json&#39;. Utilizzando Sling, la richiesta viene trasmessa al `DefaultSocialGetServlet`.

**`DefaultSocialGetServlet`**

1. Passa la risorsa (resourceType) al `SocialComponentFactoryManager` e riceve una SocialComponentFactory in grado di selezionare un `SocialComponent` rappresenta la risorsa.

1. Richiama la fabbrica e riceve un `SocialComponent` in grado di gestire la risorsa e la richiesta.
1. Richiama il `SocialComponent`, che elabora la richiesta e restituisce una rappresentazione JSON dei risultati.
1. Restituisce la risposta JSON al client.

**`GET Request`**

Un servlet di GET predefinito ascolta le richieste .social.json alle quali SocialComponent risponde con JSON personalizzabile.

![quadro di scf](assets/scf-framework.png)

### API HTTP - Richieste POST {#http-api-post-requests}

Oltre alle operazioni di GET (lettura), il framework definisce un pattern di endpoint per abilitare altre operazioni su un componente, tra cui Crea, Aggiorna ed Elimina. Questi endpoint sono API HTTP che accettano l’input e rispondono con codici di stato HTTP o con un oggetto di risposta JSON.

Questo modello di endpoint framework rende le operazioni CUD estensibili, riutilizzabili e testabili.

**`POST Request`**

È presente un’operazione Sling POST:operation per ogni operazione SocialComponent. Il codice di logica di business e manutenzione per ogni operazione è racchiuso in un OperationService accessibile tramite l’API HTTP o da un’altra posizione come servizio OSGi. Sono forniti hook che supportano le estensioni del funzionamento collegabili per le azioni prima/dopo.

![scf-post-richiesta](assets/scf-post-request.png)

### Provider di risorse di storage (SRP) {#storage-resource-provider-srp}

Per informazioni sulla gestione di UGC memorizzati nel [archivio dei contenuti della community](working-with-srp.md), vedi:

* [Panoramica del provider di risorse di storage](srp.md) - Introduzione e panoramica sull’utilizzo dell’archivio.
* [Essenze SRP e UGC](srp-and-ugc.md) - Metodi ed esempi di utilità dell’API SRP.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - Linee guida per la codifica.

### Personalizzazioni lato server {#server-side-customizations}

Visita [Personalizzazioni lato server](server-customize.md) per informazioni su come personalizzare la logica di business e il comportamento di un componente Communities sul lato server.

## Handlebar JS Lingua Di Modello {#handlebars-js-templating-language}

Una delle modifiche più evidenti nel nuovo framework è l&#39;utilizzo del `Handlebars JS` (HBS)linguaggio di modellazione, una popolare tecnologia open-source per il rendering server-client.

Gli script HBS sono semplici, senza logica, compilati sia sul server che sul client, sono facili da sovrapporre e personalizzare e si legano naturalmente con l&#39;UX client, perché HBS supporta il rendering lato client.

Il quadro fornisce diversi [Helper manubri](handlebars-helpers.md) utili nello sviluppo di componenti social.

Sul server, quando Sling risolve una richiesta di GET, identifica lo script che verrà utilizzato per rispondere alla richiesta. Se lo script è un modello HBS (.hbs), Sling delegherà la richiesta al motore Handlebars. Il motore Handlebars riceve quindi il SocialComponent dalla SocialComponentFactory appropriata, crea un contesto ed esegue il rendering di HTML.

### Nessuna limitazione di accesso {#no-access-restriction}

I file modello Handlebars (HBS) (.hbs) sono analoghi ai file modello .jsp e .html , tranne per il fatto che possono essere utilizzati per il rendering sia nel browser client che sul server. Pertanto, un browser client che richiede un modello lato client riceverà un file .hbs dal server.

Questo richiede che tutti i modelli HBS nel percorso di ricerca sling (qualsiasi file .hbs sotto /libs/ o /apps) possano essere recuperati da qualsiasi utente dall&#39;autore o pubblicazione.

L’accesso HTTP ai file .hbs potrebbe non essere vietato.

### Aggiungere o includere un componente Community {#add-or-include-a-communities-component}

La maggior parte dei componenti di Communities deve essere *aggiunto* come risorsa indirizzabile Sling. Alcuni dei componenti di Communities possono essere *incluso* in un modello come risorsa non esistente per consentire l’inclusione dinamica e la personalizzazione della posizione in cui scrivere il contenuto generato dall’utente (UGC).

In entrambi i casi, il [librerie client richieste](clientlibs.md) Deve essere presente anche.

**Aggiungere un componente**

L’aggiunta di un componente si riferisce al processo di aggiunta di un’istanza di una risorsa (componente), ad esempio se trascinata dal browser Componenti (barra laterale) su una pagina in modalità di modifica dell’autore.

Il risultato è un nodo figlio JCR sotto un nodo par, che è indirizzabile Sling.

**Includere un componente**

L’inclusione di un componente si riferisce al processo di aggiunta di un riferimento a un [risorsa &quot;non esistente&quot;](srp.md#for-non-existing-resources-ners) (nessun nodo JCR) all&#39;interno del modello, ad esempio utilizzando un linguaggio di script.

A partire da AEM 6.1, quando un componente viene incluso dinamicamente invece che aggiunto, è possibile modificare le proprietà del componente nel modo autore *design *.

Solo alcuni componenti di AEM Communities possono essere inclusi in modo dinamico. Sono:

* [Commenti](essentials-comments.md)
* [Valutazione](rating-basics.md)
* [Recensioni](reviews-basics.md)
* [Votazione](essentials-voting.md)

La [Guida ai componenti della community](components-guide.md) consente di attivare o disattivare l’aggiunta dei componenti inclusi all’inclusione.

**Quando si utilizzano le barre manuali** linguaggio di template, la risorsa non esistente è inclusa utilizzando [includi aiuto](handlebars-helpers.md#include) specificando il relativo resourceType:

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**Quando si utilizza JSP**, una risorsa viene inclusa utilizzando il tag [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>Per aggiungere un componente a una pagina in modo dinamico, anziché aggiungerlo o includerlo in un modello, consulta [Caricamento laterale componente](sideloading.md).

### Helper manubri {#handlebars-helpers}

Vedi [Helper manubrio SCF](handlebars-helpers.md) per un elenco e una descrizione degli helper personalizzati disponibili in SCF.

## Framework lato client {#client-side-framework}

### Framework Javascript Vista Modello {#model-view-javascript-framework}

Il quadro include un&#39;estensione del [Backbone.js](https://www.backbonejs.org/), un framework JavaScript per la visualizzazione modello, per facilitare lo sviluppo di componenti interattivi avanzati. La natura orientata agli oggetti supporta un framework estensibile/riutilizzabile. La comunicazione tra client e server viene semplificata tramite l’API HTTP.

Il framework sfrutta i modelli Handlebars lato server per eseguire il rendering dei componenti per il client. I modelli si basano sulle risposte JSON generate dall’API HTTP. Le visualizzazioni si associano ad HTML generate dai modelli Handlebars e forniscono interattività.

### Convenzioni CSS {#css-conventions}

Di seguito sono riportate le convenzioni consigliate per definire e utilizzare le classi CSS:

* Utilizza nomi di selettore classe CSS chiaramente spaccati ed evita nomi generici come &quot;intestazione&quot;, &quot;immagine&quot;, ecc.
* Definisci stili di selettore classe specifici in modo che i fogli di stile CSS funzionino bene con altri elementi e stili sulla pagina. Esempio: `.social-forum .topic-list .li { color: blue; }`
* Separa le classi CSS per lo stile dalle classi CSS per gli UX guidate da JavaScript.

### Personalizzazioni lato client {#client-side-customizations}

Per personalizzare l’aspetto e il comportamento di un componente Community sul lato client, fai riferimento a [Personalizzazioni lato client](client-customize.md), che include informazioni su:

* [Sovrapposizioni](client-customize.md#overlays)
* [Estensioni](client-customize.md#extensions)
* [Markup HTML](client-customize.md#htmlmarkup)
* [Skin CSS](client-customize.md#skinning-css)
* [Estensione Javascript](client-customize.md#extending-javascript)
* [Clientlibs per SCF](client-customize.md#clientlibs-for-scf)

## Funzionalità e componenti di base {#feature-and-component-essentials}

Le informazioni essenziali per gli sviluppatori sono descritte nella sezione [Funzionalità e componenti di base](essentials.md) sezione .

Ulteriori informazioni per gli sviluppatori sono disponibili nella sezione [Linee guida sulla codifica](code-guide.md) sezione .

## Risoluzione dei problemi {#troubleshooting}

Le preoccupazioni comuni e i problemi noti sono descritti nella [Risoluzione dei problemi](troubleshooting.md) sezione .
