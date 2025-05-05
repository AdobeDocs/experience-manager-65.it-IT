---
title: Framework componenti social
description: Il framework dei componenti social (SCF) semplifica il processo di configurazione, personalizzazione ed estensione dei componenti Community
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 5ca58bc3-8505-4d91-9cd1-6b2e2671f1be
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1478'
ht-degree: 0%

---

# Framework componenti social {#social-component-framework}

Il framework dei componenti social (SCF) semplifica il processo di configurazione, personalizzazione ed estensione dei componenti Community sia sul lato server che sul lato client.

Vantaggi del quadro:

* **Funzionale**: facilità di integrazione preconfigurata con poca o nessuna personalizzazione per l&#39;80% dei casi d&#39;uso.
* **Skinnable**: utilizzo coerente degli attributi HTML per lo stile CSS.
* **Estendibile**: l&#39;implementazione dei componenti è orientata agli oggetti e si basa su una logica di business leggera: è facile aggiungere l&#39;accesso aziendale incrementale al server.
* **Flessibile**: semplici modelli JavaScript senza logica facilmente sovrapposti e personalizzati.
* **Accessibile**: l&#39;API HTTP supporta la pubblicazione da qualsiasi client, incluse le app mobili.
* **Portatile**: integra/incorpora in qualsiasi pagina Web basata su qualsiasi tecnologia.

Esplora in un&#39;istanza di authoring o pubblicazione utilizzando la [guida interattiva ai componenti della community](components-guide.md).

## Panoramica {#overview}

In SCF, un componente è composto da un POJO SocialComponent, un Modello JS Handlebars (per riprodurre il componente) e CSS (per formattare il componente).

Un modello JS Handlebars può estendere i componenti JS del modello/vista per gestire l’interazione dell’utente con il componente sul client.

Se un componente deve supportare la modifica dei dati, l’implementazione dell’API SocialComponent può essere scritta per supportare la modifica o il salvataggio di dati in modo simile agli oggetti modello/dati nelle applicazioni web tradizionali. Inoltre, è possibile aggiungere operazioni (controller) e un servizio operativo per gestire le richieste di operazioni, eseguire la logica di business e richiamare le API sugli oggetti modello/dati.

L’API SocialComponent può essere estesa per fornire i dati richiesti da un client per un livello di visualizzazione o un client HTTP.

### Rendering delle pagine per il client {#how-pages-are-rendered-for-client}

![rendering pagina-scf](assets/scf-overview.png)

### Personalizzazione ed estensione dei componenti {#component-customization-and-extension}

Per personalizzare o estendere i componenti, scrivi solo le sovrapposizioni e le estensioni nella directory /apps, semplificando il processo di aggiornamento alle versioni future.

* Per lo skin:
   * Solo il file CSS [deve essere modificato](client-customize.md#skinning-css).
* Per aspetto:
   * Modifica il modello JS e il CSS.
* Per Look, Feel e UX:
   * Modificare il modello JS, CSS e [estendere/sostituire JavaScript](client-customize.md#extending-javascript).
* Per modificare le informazioni disponibili per il modello JS o per l’endpoint GET:
   * Estendere [SocialComponent](server-customize.md#socialcomponent-interface).
* Per aggiungere l&#39;elaborazione personalizzata durante le operazioni:
   * Scrivere un [OperationExtension](server-customize.md#operationextension-class).
* Per aggiungere un&#39;operazione personalizzata:
   * Crea un&#39;operazione Sling Post [&#128279;](server-customize.md#postoperation-class).
   * Utilizza [OperationServices](server-customize.md#operationservice-class) esistente in base alle esigenze.
   * Aggiungi il codice JavaScript per richiamare l’operazione dal lato client in base alle esigenze.

## Framework lato server {#server-side-framework}

Il framework fornisce API per accedere alle funzionalità sul server e supportare l’interazione tra client e server.

### API Java™ {#java-apis}

Le API Java™ forniscono classi e interfacce astratte che vengono facilmente ereditate o sottoclassificate.

Le classi principali sono descritte nella pagina [Personalizzazione lato server](server-customize.md).

Visita [Panoramica del provider di risorse di archiviazione](srp.md) per informazioni sull&#39;utilizzo di UGC.

### API HTTP {#http-api}

L&#39;API HTTP supporta la facilità di personalizzazione e la scelta delle piattaforme client per le app PhoneGap, le app native e altre integrazioni e mashup. Inoltre, l’API HTTP consente a un sito della community di funzionare come servizio senza un client, in modo tale che i componenti del framework possano essere integrati in qualsiasi pagina web basata su qualsiasi tecnologia.

### API HTTP - Richieste GET {#http-api-get-requests}

Per ogni SocialComponent, il framework fornisce un endpoint API basato su HTTP. L’endpoint è accessibile inviando una richiesta GET alla risorsa con un selettore &quot;.social.json&quot; e un’estensione. Utilizzando Sling, la richiesta viene trasmessa a `DefaultSocialGetServlet`.

**`DefaultSocialGetServlet`**

1. Passa la risorsa (resourceType) a `SocialComponentFactoryManager` e riceve un SocialComponentFactory in grado di selezionare un `SocialComponent` che rappresenta la risorsa.

1. Richiama la factory e riceve un `SocialComponent` in grado di gestire la risorsa e la richiesta.
1. Richiama `SocialComponent`, che elabora la richiesta e restituisce una rappresentazione JSON dei risultati.
1. Restituisce la risposta JSON al client.

**`GET Request`**

Un servlet di GET predefinito ascolta le richieste .social.json alle quali il componente Social risponde con JSON personalizzabile.

![scf-framework](assets/scf-framework.png)

### API HTTP - Richieste POST {#http-api-post-requests}

Oltre alle operazioni di GET (lettura), il framework definisce un modello di endpoint per abilitare altre operazioni su un componente, tra cui Crea, Aggiorna ed Elimina. Questi endpoint sono API HTTP che accettano input e rispondono con un codice di stato HTTP o con un oggetto di risposta JSON.

Questo modello di endpoint framework rende le operazioni CUD estensibili, riutilizzabili e testabili.

**`POST Request`**

È disponibile un’operazione Sling POST:per ogni operazione SocialComponent. La logica di business e il codice di manutenzione per ogni operazione sono racchiusi in un OperationService accessibile tramite l’API HTTP o da altrove come servizio OSGi. Gli hook sono forniti con supporto di estensioni di operazioni collegabili per le azioni prima/dopo.

![scf-post-richiesta](assets/scf-post-request.png)

### Provider risorsa di archiviazione (SRP) {#storage-resource-provider-srp}

Per informazioni sulla gestione dei contenuti generati dagli utenti archiviati nell&#39;[archivio dei contenuti della community](working-with-srp.md), vedere:

* [Panoramica del provider di risorse di archiviazione](srp.md) - Introduzione e panoramica sull&#39;utilizzo dell&#39;archivio.
* [Nozioni di base su SRP e UGC](srp-and-ugc.md) - Metodi ed esempi dell&#39;utilità API SRP.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - Linee guida per la codifica.

### Personalizzazioni lato server {#server-side-customizations}

Visita [Personalizzazioni lato server](server-customize.md) per informazioni sulla personalizzazione della logica di business e del comportamento di un componente Communities sul lato server.

## Linguaggio del modello JS Handlebars {#handlebars-js-templating-language}

Una delle modifiche più rilevanti del nuovo framework è l&#39;utilizzo del linguaggio di modelli `Handlebars JS` (HBS), una tecnologia open-source per il rendering server-client.

Gli script HBS sono semplici, senza logica, sono compilati sia sul server che sul client, sono facili da sovrapporre e personalizzare e si associano naturalmente all&#39;interfaccia utente del client perché HBS supporta il rendering lato client.

Il framework fornisce diversi [Helper Handlebars](handlebars-helpers.md) che sono utili per lo sviluppo di SocialComponents.

Sul server, quando Sling risolve una richiesta GET, identifica lo script utilizzato per rispondere alla richiesta. Se lo script è un modello HBS (con estensione hbs), Sling delegherà la richiesta al motore Handlebars. Il motore Handlebars otterrà quindi il componente SocialComponent dal SocialComponentFactory appropriato, creerà un contesto ed eseguirà il rendering del HTML.

### Nessuna restrizione di accesso {#no-access-restriction}

I file di modello Handlebars (HBS) sono simili ai file di modello .jsp e .html, ma possono essere utilizzati per il rendering sia nel browser client che nel server. Pertanto, un browser client che richiede un modello lato client riceve un file con estensione hbs dal server.

Questo richiede che tutti i modelli HBS nel percorso di ricerca sling (qualsiasi file .hbs in /libs/ o /apps) possano essere recuperati da qualsiasi utente dall’ambiente di authoring o pubblicazione.

L&#39;accesso HTTP ai file con estensione hbs non può essere vietato.

### Aggiungere o includere un componente community {#add-or-include-a-communities-component}

La maggior parte dei componenti di Communities deve essere *aggiunto* come risorsa indirizzabile Sling. Alcuni componenti di Communities possono essere *inclusi* in un modello come risorsa non esistente per consentire l&#39;inclusione e la personalizzazione dinamiche della posizione in cui scrivere contenuti generati dall&#39;utente (UGC, User-Generated Content).

In entrambi i casi, devono essere presenti anche le [librerie client richieste](clientlibs.md) del componente.

**Aggiungi un componente**

L’aggiunta di un componente si riferisce al processo di aggiunta di un’istanza di una risorsa (componente), ad esempio quando viene trascinata dal browser Componenti (barra laterale) in una pagina in modalità di modifica dell’autore.

Il risultato è un nodo figlio JCR sotto un nodo par, che è indirizzabile Sling.

**Includi un componente**

L&#39;inclusione di un componente si riferisce al processo di aggiunta di un riferimento a una risorsa [&quot;non esistente&quot;](srp.md#for-non-existing-resources-ners) (nessun nodo JCR) all&#39;interno del modello, ad esempio l&#39;utilizzo di un linguaggio di script.

A partire da Adobe Experience Manager (AEM) 6.1, quando un componente viene incluso dinamicamente anziché aggiunto, è possibile modificarne le proprietà in modalità di creazione *progettazione*.

Solo alcuni componenti di AEM Communities possono essere inclusi in modo dinamico. Sono:

* [Commenti](essentials-comments.md)
* [Valutazione](rating-basics.md)
* [Recensioni](reviews-basics.md)
* [Votazione](essentials-voting.md)

La [Guida ai componenti della community](components-guide.md) consente di impedire l&#39;aggiunta e l&#39;inclusione di componenti inclusi.

**Quando si utilizza il linguaggio di modelli Handlebars**, la risorsa non esistente viene inclusa utilizzando l&#39;helper [include](handlebars-helpers.md#include) specificando il relativo resourceType:

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**Quando si utilizza JSP**, viene inclusa una risorsa utilizzando il tag [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>Per aggiungere un componente a una pagina in modo dinamico, invece di aggiungerlo o includerlo in un modello, vedere [Componente - Sideloading](sideloading.md).

### Helper Handlebars {#handlebars-helpers}

Per un elenco e una descrizione degli helper personalizzati disponibili in SCF, consulta [Helper Handlebars SCF](handlebars-helpers.md).

## Framework lato client {#client-side-framework}

### Framework JavaScript vista modello {#model-view-javascript-framework}

Il framework include un&#39;estensione di [Backbone.js](https://backbonejs.org/), un framework JavaScript per la visualizzazione del modello, per facilitare lo sviluppo di componenti avanzati e interattivi. La natura orientata agli oggetti supporta un framework estensibile/riutilizzabile. La comunicazione tra client e server è semplificata con l’API HTTP.

Il framework utilizza modelli Handlebars lato server per eseguire il rendering dei componenti per il client. I modelli si basano sulle risposte JSON generate dall’API HTTP. Le visualizzazioni si associano a HTML generate dai modelli Handlebars e forniscono interattività.

### Convenzioni CSS {#css-conventions}

Di seguito sono riportate le convenzioni consigliate per la definizione e l’utilizzo delle classi CSS:

* Utilizza nomi selettori di classi CSS con spazi chiari ed evita nomi generici come &quot;intestazione&quot; e &quot;immagine&quot;.
* Definisci stili selettori di classe specifici in modo che i fogli di stile CSS funzionino correttamente con altri elementi e stili nella pagina. Esempio: `.social-forum .topic-list .li { color: blue; }`
* Mantenere le classi CSS per lo stile separate dalle classi CSS per l&#39;interfaccia utente guidata da JavaScript.

### Personalizzazioni lato client {#client-side-customizations}

Per personalizzare l&#39;aspetto e il comportamento di un componente Communities sul lato client, fare riferimento a [Personalizzazioni sul lato client](client-customize.md), che include informazioni su:

* [Sovrapposizioni](client-customize.md#overlays)
* [Estensioni](client-customize.md#extensions)
* [Markup HTML](client-customize.md#htmlmarkup)
* [CSS interfaccia](client-customize.md#skinning-css)
* [Estensione di JavaScript](client-customize.md#extending-javascript)
* [Clientlibs per SCF](client-customize.md#clientlibs-for-scf)

## Funzionalità e componenti essenziali {#feature-and-component-essentials}

Le informazioni essenziali per gli sviluppatori sono descritte nella sezione [Funzionalità e componenti essenziali](essentials.md).

Ulteriori informazioni per gli sviluppatori sono disponibili nella sezione [Coding Guidelines](code-guide.md).

## Risoluzione dei problemi {#troubleshooting}

I problemi comuni e noti sono descritti nella sezione [Risoluzione dei problemi](troubleshooting.md).
