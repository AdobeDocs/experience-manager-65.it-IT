---
title: Framework componenti social
seo-title: Social Component Framework
description: Il framework dei componenti social (SCF) semplifica il processo di configurazione, personalizzazione ed estensione dei componenti Community
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

# Framework componenti social {#social-component-framework}

Il framework dei componenti social (SCF) semplifica il processo di configurazione, personalizzazione ed estensione dei componenti Community sia sul lato server che sul lato client.

Vantaggi del quadro:

* **Funzionale**: facilità di integrazione preconfigurata con poca o nessuna personalizzazione per l’80% dei casi d’uso.
* **Skinnable**: utilizzo coerente degli attributi HTML per lo stile CSS.
* **Estendibile**: l’implementazione dei componenti è orientata agli oggetti e semplice da usare per la logica di business, per aggiungere facilmente un accesso aziendale incrementale al server.
* **Flessibile**: semplici modelli JavaScript senza logica facilmente sovrapposti e personalizzati.
* **Accessibile**: l’API HTTP supporta la pubblicazione da qualsiasi client, incluse le app mobili.
* **Portatile**: integra/incorpora in qualsiasi pagina web basata su qualsiasi tecnologia.

Esplorare in un’istanza di authoring o pubblicazione utilizzando il [Guida ai componenti della community](components-guide.md).

## Panoramica {#overview}

In SCF, un componente è composto da un POJO SocialComponent, un Modello JS Handlebars (per riprodurre il componente) e CSS (per formattare il componente).

Un modello JS Handlebars può estendere i componenti JS del modello/vista per gestire l’interazione dell’utente con il componente sul client.

Se un componente deve supportare la modifica dei dati, l’implementazione dell’API SocialComponent può essere scritta per supportare la modifica o il salvataggio di dati in modo simile agli oggetti modello/dati nelle applicazioni web tradizionali. Inoltre, è possibile aggiungere operazioni (controller) e un servizio operativo per gestire le richieste di operazioni, eseguire la logica di business e richiamare le API sugli oggetti modello/dati.

L’API SocialComponent può essere estesa per fornire i dati richiesti da un client per un livello di visualizzazione o un client HTTP.

### Rendering delle pagine per il client {#how-pages-are-rendered-for-client}

![scf-page-rendering](assets/scf-overview.png)

### Personalizzazione ed estensione dei componenti {#component-customization-and-extension}

Per personalizzare o estendere i componenti, scrivi solo le sovrapposizioni e le estensioni nella directory /apps, semplificando il processo di aggiornamento alle versioni future.

* Per lo skin:
   * Solo il [CSS deve essere modificato](client-customize.md#skinning-css).
* Per aspetto:
   * Modifica il modello JS e il CSS.
* Per Look, Feel e UX:
   * Modificare il modello JS, CSS e [estendere/sostituire JavaScript](client-customize.md#extending-javascript).
* Per modificare le informazioni disponibili per il modello JS o per l’endpoint GET:
   * Estendi il [ComponenteSocial](server-customize.md#socialcomponent-interface).
* Per aggiungere l&#39;elaborazione personalizzata durante le operazioni:
   * Scrivi un [OperationExtension](server-customize.md#operationextension-class).
* Per aggiungere una nuova operazione personalizzata:
   * Crea un nuovo [Operazione di post Sling](server-customize.md#postoperation-class).
   * Usa esistente [OperationServices](server-customize.md#operationservice-class) secondo necessità.
   * Aggiungi codice JavaScript per richiamare l’operazione dal lato client in base alle esigenze.

## Framework lato server {#server-side-framework}

Il framework fornisce API per accedere alle funzionalità sul server e supportare l’interazione tra client e server.

### API Java {#java-apis}

Le API Java forniscono classi e interfacce astratte che vengono facilmente ereditate o sottoclassificate.

Le classi principali sono descritte nella [Personalizzazione lato server](server-customize.md) pagina.

Visita [Panoramica del provider di risorse di archiviazione](srp.md) per scoprire come utilizzare UGC.

### API HTTP {#http-api}

L&#39;API HTTP supporta la facilità di personalizzazione e la scelta delle piattaforme client per le app PhoneGap, le app native e altre integrazioni e mashup. Inoltre, l’API HTTP consente a un sito della community di funzionare come servizio senza un client, in modo tale che i componenti del framework possano essere integrati in qualsiasi pagina web basata su qualsiasi tecnologia.

### API HTTP - Richieste GET {#http-api-get-requests}

Per ogni SocialComponent, il framework fornisce un endpoint API basato su HTTP. L’endpoint è accessibile inviando una richiesta GET alla risorsa con un selettore &quot;.social.json&quot; e un’estensione. Utilizzando Sling, la richiesta viene trasmessa al `DefaultSocialGetServlet`.

**`DefaultSocialGetServlet`**

1. Passa la risorsa (resourceType) al `SocialComponentFactoryManager` e riceve un oggetto SocialComponentFactory in grado di selezionare `SocialComponent` che rappresenta la risorsa.

1. Richiama la fabbrica e riceve un `SocialComponent` in grado di gestire la risorsa e la richiesta.
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

![scf-post-request](assets/scf-post-request.png)

### Provider risorsa di archiviazione (SRP) {#storage-resource-provider-srp}

Per informazioni sulla gestione di contenuti generati dagli utenti archiviati in [archivio contenuti community](working-with-srp.md), vedi:

* [Panoramica del provider di risorse di archiviazione](srp.md) - Introduzione e panoramica sull’utilizzo dell’archivio.
* [Nozioni di base su SRP e UGC](srp-and-ugc.md) - Metodi ed esempi di utilità API SRP.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - Linee guida per la codifica.

### Personalizzazioni lato server {#server-side-customizations}

Visita [Personalizzazioni lato server](server-customize.md) per informazioni sulla personalizzazione della logica di business e del comportamento di un componente Communities sul lato server.

## Linguaggio del modello JS Handlebars {#handlebars-js-templating-language}

Uno dei cambiamenti più significativi del nuovo assetto è l&#39;uso del `Handlebars JS` (HBS), un popolare linguaggio open-source per il rendering server-client.

Gli script HBS sono semplici, senza logica, sono compilati sia sul server che sul client, sono facili da sovrapporre e personalizzare e si associano naturalmente all&#39;interfaccia utente del client perché HBS supporta il rendering lato client.

Il framework fornisce diversi [Handlebars Helpers](handlebars-helpers.md) utili per lo sviluppo di SocialComponents.

Sul server, quando Sling risolve una richiesta GET, identifica lo script che verrà utilizzato per rispondere alla richiesta. Se lo script è un modello HBS (con estensione hbs), Sling delegherà la richiesta al motore Handlebars. Il motore Handlebars otterrà quindi il componente SocialComponent dal SocialComponentFactory appropriato, creerà un contesto ed eseguirà il rendering del HTML.

### Nessuna restrizione di accesso {#no-access-restriction}

I file di modello Handlebars (HBS) sono simili ai file di modello .jsp e .html, ma possono essere utilizzati per il rendering sia nel browser client che nel server. Pertanto, un browser client che richiede un modello lato client riceverà un file con estensione hbs dal server.

Questo richiede che tutti i modelli HBS nel percorso di ricerca sling (qualsiasi file .hbs in /libs/ o /apps) possano essere recuperati da qualsiasi utente dall’ambiente di authoring o pubblicazione.

L&#39;accesso HTTP ai file con estensione hbs non può essere vietato.

### Aggiungere o includere un componente community {#add-or-include-a-communities-component}

La maggior parte dei componenti di Communities deve essere *aggiunto* come risorsa indirizzabile Sling. È possibile che alcuni dei componenti di Communities siano *incluso* in un modello come risorsa non esistente per consentire l’inclusione dinamica e la personalizzazione della posizione in cui scrivere il contenuto generato dall’utente (UGC, User Generated Content).

In entrambi i casi, i [librerie client richieste](clientlibs.md) deve essere presente anche.

**Aggiungi un componente**

L’aggiunta di un componente si riferisce al processo di aggiunta di un’istanza di una risorsa (componente), ad esempio quando viene trascinata dal browser Componenti (barra laterale) in una pagina in modalità di modifica dell’autore.

Il risultato è un nodo figlio JCR sotto un nodo par, che è indirizzabile Sling.

**Includi un componente**

L&#39;inclusione di un componente si riferisce al processo di aggiunta di un riferimento a un [risorsa &quot;non esistente&quot;](srp.md#for-non-existing-resources-ners) (nessun nodo JCR) all’interno del modello, ad esempio utilizzando un linguaggio di script.

A partire da AEM 6.1, quando un componente viene incluso dinamicamente invece che aggiunto, è possibile modificare le proprietà del componente in modalità author *design *.

Solo alcuni componenti di AEM Communities possono essere inclusi in modo dinamico. Sono:

* [Commenti](essentials-comments.md)
* [Valutazione](rating-basics.md)
* [Recensioni](reviews-basics.md)
* [Votazione](essentials-voting.md)

Il [Guida ai componenti della community](components-guide.md) consente di impostare l’aggiunta o l’inclusione di componenti inclusi.

**Quando si utilizza Handlebars** lingua dei modelli, la risorsa non esistente viene inclusa utilizzando [include helper](handlebars-helpers.md#include) specificando il relativo resourceType:

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**Quando si utilizza JSP**, viene inclusa una risorsa utilizzando il tag [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>Per aggiungere un componente a una pagina in modo dinamico, invece di aggiungerlo o includerlo in un modello, vedi [Caricamento laterale componente](sideloading.md).

### Helper Handlebars {#handlebars-helpers}

Consulta [Helper Handlebars SCF](handlebars-helpers.md) per un elenco e una descrizione degli helper personalizzati disponibili in SCF.

## Framework lato client {#client-side-framework}

### Framework JavaScript Visualizzazione Modello {#model-view-javascript-framework}

Il quadro comprende un&#39;estensione [Backbone.js](https://www.backbonejs.org/), framework JavaScript per la visualizzazione del modello, per facilitare lo sviluppo di componenti avanzati e interattivi. La natura orientata agli oggetti supporta un framework estensibile/riutilizzabile. La comunicazione tra client e server è semplificata tramite l’API HTTP.

Il framework sfrutta i modelli Handlebars lato server per eseguire il rendering dei componenti per il client. I modelli si basano sulle risposte JSON generate dall’API HTTP. Le visualizzazioni si associano a HTML generate dai modelli Handlebars e forniscono interattività.

### Convenzioni CSS {#css-conventions}

Di seguito sono riportate le convenzioni consigliate per la definizione e l’utilizzo delle classi CSS:

* Utilizza nomi selettori di classi CSS con spazi chiari ed evita nomi generici come &quot;intestazione&quot;, &quot;immagine&quot;, ecc.
* Definisci stili selettori di classe specifici in modo che i fogli di stile CSS funzionino correttamente con altri elementi e stili nella pagina. Esempio: `.social-forum .topic-list .li { color: blue; }`
* Mantenere le classi CSS per lo stile separate dalle classi CSS per l&#39;interfaccia utente guidata da JavaScript.

### Personalizzazioni lato client {#client-side-customizations}

Per personalizzare l&#39;aspetto e il comportamento di un componente Communities sul lato client, fare riferimento a [Personalizzazioni lato client](client-customize.md), che include informazioni su:

* [Sovrapposizioni](client-customize.md#overlays)
* [Estensioni](client-customize.md#extensions)
* [Markup HTML](client-customize.md#htmlmarkup)
* [CSS interfaccia](client-customize.md#skinning-css)
* [Estensione di JavaScript](client-customize.md#extending-javascript)
* [Clientlibs per SCF](client-customize.md#clientlibs-for-scf)

## Funzionalità e componenti essenziali {#feature-and-component-essentials}

Le informazioni essenziali per gli sviluppatori sono descritte nella sezione [Funzionalità e componenti essenziali](essentials.md) sezione.

Ulteriori informazioni per gli sviluppatori sono disponibili nella [Linee guida per la codifica](code-guide.md) sezione.

## Risoluzione dei problemi {#troubleshooting}

I problemi comuni e quelli noti sono descritti nel [Risoluzione dei problemi](troubleshooting.md) sezione.
