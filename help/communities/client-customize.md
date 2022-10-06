---
title: Personalizzazione lato client
seo-title: Client-side Customization
description: Personalizzazione del comportamento o dell’aspetto lato client in AEM Communities
seo-description: Customizing behavior or appearance client-side in AEM Communities
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
exl-id: bf34f564-ac93-4c8c-95f7-8690d99d85cb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---

# Personalizzazione lato client  {#client-side-customization}

| **[⇐ funzioni di base](essentials.md)** | **[Informazioni sulla personalizzazione lato server](server-customize.md)** |
|---|---|
|  | **[Helpers Handlebars SCF](handlebars-helpers.md)** |

Per personalizzare l’aspetto e/o il comportamento di un componente AEM Communities sul lato client, sono disponibili diversi approcci.

Due approcci principali consistono nel sovrapporre o estendere un componente.

[Sovrapposizione](#overlays) un componente modifica il componente predefinito e influenza ogni riferimento al componente.

[Estensione](#extensions) un componente, denominato in modo univoco, limita l’ambito delle modifiche. Il termine &#39;extension&#39; viene utilizzato in modo intercambiabile con &#39;override&#39;.

## Sovrapposizioni {#overlays}

La sovrapposizione di un componente è un metodo per apportare modifiche a un componente predefinito e interessa tutte le istanze che utilizzano l’impostazione predefinita.

La sovrapposizione viene eseguita modificando una copia del componente predefinito nel /**app** anziché modificare il componente originale nel /**libs** directory. Il componente è costruito con un percorso relativo identico, ad eccezione di &quot;libs&quot; viene sostituito con &quot;apps&quot;.

La directory /apps è la prima posizione in cui viene eseguita la ricerca per risolvere le richieste e, se non viene trovata, viene utilizzata la versione predefinita presente nella directory /libs .

Il componente predefinito nella directory /libs non deve mai essere modificato in quanto le patch e gli aggiornamenti futuri sono liberi di modificare la directory /libs in qualsiasi modo necessario durante la manutenzione delle interfacce pubbliche.

Questo è diverso da [estensione](#extensions) un componente predefinito in cui si desidera apportare modifiche per un uso specifico, creare un percorso univoco del componente e fare riferimento al componente predefinito originale nella directory /libs come tipo di risorsa eccellente.

Per un rapido esempio di sovrapposizione del componente commenti, prova il [Esercitazione sul componente Sovrapponi commenti](overlay-comments.md).

## Estensioni {#extensions}

L’estensione (override) di un componente è un metodo per apportare modifiche per un uso specifico senza influire su tutte le istanze che utilizzano l’impostazione predefinita. Il componente esteso è denominato in modo univoco nella cartella /apps e fa riferimento al componente predefinito nella cartella /libs , pertanto la progettazione e il comportamento predefiniti di un componente non vengono modificati.

Questo è diverso da [sovrapposizione](#overlays) il componente predefinito in cui la natura di Sling risolve i riferimenti relativi alle app/cartella prima di eseguire la ricerca nella cartella libs/ , in modo che la progettazione o il comportamento di un componente vengano modificati a livello globale.

Per un rapido esempio di estensione del componente commenti, prova la [Esercitazione sul componente Estendi commenti](extend-comments.md).

## Binding Javascript {#javascript-binding}

Lo script HBS per il componente deve essere associato agli oggetti, ai modelli e alle visualizzazioni JavaScript che implementano questa funzione.

Il valore del `data-scf-component` può essere l&#39;attributo predefinito, ad esempio **`social/tally/components/hbs/rating`** o un componente esteso (personalizzato) per funzionalità personalizzate, ad esempio **weretail/components/hbs/rating**.

Per eseguire un binding di un componente, l’intero script del componente deve essere racchiuso in un &lt;div> con i seguenti attributi:

* `data-component-id`=&quot;{{id}}&quot;

   viene risolto nella proprietà id dal contesto

* `data-scf-component`=&quot;*&lt;resourcetype>*

Ad esempio, da `/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="{{id}}" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## Proprietà personalizzate {#custom-properties}

Quando si estende o si sovrappone un componente, è possibile aggiungere proprietà a una finestra di dialogo modificata.

È possibile accedere a tutte le proprietà impostate su un componente/risorsa facendo riferimento alle chiavi di proprietà nel modello handlebars:

`{{properties.<property_name>}}`

## Skin CSS {#skinning-css}

La personalizzazione dei componenti in base al tema generale del sito web può essere ottenuta mediante la &quot;skin&quot;: cambiare colori, font, immagini, pulsanti, collegamenti, spaziatura e persino posizionamento in una certa misura.

La skin può essere ottenuta ignorando selettivamente gli stili del framework o scrivendo fogli di stile completamente nuovi. I componenti SCF definiscono classi CSS con spazi dei nomi, modulari e semantiche che influiscono sui vari elementi che compongono un componente.

Per applicare uno skin a un componente:

1. Identifica gli elementi che desideri modificare (ad esempio area compositore, pulsanti della barra degli strumenti, font del messaggio, ecc.).
1. Identifica le classi/regole CSS che influiscono su questi elementi.
1. Creare un file foglio di stile (.css).
1. Includere il foglio di stile in una cartella della libreria client ([clientlibs](#clientlibs-for-scf)) per il sito e accertati che sia incluso nei modelli e nelle pagine con [ui:includeClientLib](../../help/sites-developing/clientlibs.md).

1. Ridefinire le classi e le regole CSS identificate (#2) nel foglio di stile e aggiungere stili.

Gli stili personalizzati sostituiranno gli stili del framework predefiniti; il componente verrà riprodotto con il nuovo skin.

>[!CAUTION]
>
>Qualsiasi nome di classe CSS con prefisso `scf-js` ha un uso specifico nel codice javascript. Queste classi influiscono sullo stato di un componente (ad esempio, per passare da nascosto a visibile) e non devono essere né ignorate né rimosse.
>
>Mentre il `scf-js` le classi non influiscono sugli stili, i nomi delle classi possono essere utilizzati in fogli di stile con la consapevolezza che, dato che controllano gli stati degli elementi, ci possono essere effetti collaterali.

## Estensione Javascript {#extending-javascript}

Per estendere un’implementazione di componenti JavaScript, è necessario:

1. Crea un componente per l’app con un jcr:resourceSuperType impostato sul valore del jcr:resourceType del componente esteso, ad esempio social/forum/components/hbs/forum.
1. Esamina il codice Javascript del componente SCF predefinito per determinare quali metodi devono essere registrati utilizzando SCF.registerComponent().
1. Copia il codice JavaScript del componente esteso o inizia da zero.
1. Estendi il metodo .
1. Utilizzare SCF.registerComponent() per registrare tutti i metodi con le impostazioni predefinite o con gli oggetti e le viste personalizzati.

### forum.js: Estensione di esempio del forum - HBS  {#forum-js-sample-extension-of-forum-hbs}

```xml
(function($CQ, _, Backbone, SCF) {
    "use strict";
    var GMForumView = SCF.ForumView.extend({
        viewName: "GMForum",
        showComposer: function(e) {
            SCF.ForumView.prototype.toggleComposer.apply(this);
            var cancel = this.$el.find('.cancel-new-topic');
            cancel.toggle();
        },
        hideComposer: function(e) {
            SCF.ForumView.prototype.toggleComposer.apply(this);
            var cancel = this.$el.find('.cancel-new-topic');
            cancel.toggle();
        }
    });

    SCF.registerComponent('social/forum/components/hbs/post', SCF.Post, SCF.PostView);
    SCF.registerComponent('social/forum/components/hbs/topic', SCF.Topic, SCF.TopicView);
    SCF.registerComponent('social/forum/components/hbs/forum', SCF.Forum, GMForumView );
})($CQ, _, Backbone, SCF);
```

## Tag script {#script-tags}

I tag script sono parte integrante del framework lato client. Sono la colla che consente di associare il markup generato sul lato server ai modelli e alle visualizzazioni sul lato client.

I tag script negli script SCF non devono essere rimossi quando si sovrappongono o si ignorano i componenti. I tag script SCF creati automaticamente per l’inserimento di JSON in HTML sono identificati con l’attributo `data-scf-json=true`.

## Clientlibs per SCF {#clientlibs-for-scf}

L&#39;uso di [librerie lato client](../../help/sites-developing/clientlibs.md) (clientlibs), fornisce un mezzo per organizzare e ottimizzare JavaScript e CSS utilizzati per il rendering dei contenuti sul client.

Le clientlibs per SCF seguono un pattern di denominazione molto specifico per due varianti, che variano solo dalla presenza di &quot;author&quot; nel nome della categoria:

| Variante Clientlib | Pattern per la proprietà Categorie |
|--- |--- |
| clientlib completo | cq.social.hbs.&lt;component name> |
| clientlib autore | cq.social.author.hbs.&lt;component name> |

### Clientlibs completi {#complete-clientlibs}

Le clientlib complete (non di authoring) includono dipendenze e sono utili per l’inclusione con ui:includeClientLib.

Queste versioni si trovano in:

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

Esempio:

* Nodo cartella client: `/etc/clientlibs/social/hbs/forum`
* Proprietà Categorie: `cq.social.hbs.forum`

La [Guida ai componenti della community](components-guide.md) elenca le clientlib complete richieste per ogni componente SCF.

[Componenti Clientlibs for Communities](clientlibs.md) descrive come aggiungere clientlibs a una pagina.

### Autore Clientlibs {#author-clientlibs}

Le clientlibs della versione dell’autore vengono ridotte al minimo JavaScript necessario per implementare il componente.

Queste clientlibs non dovrebbero mai essere incluse direttamente, ma sono invece disponibili per incorporarle in altri clientlibs, creati a mano per un sito.

Queste versioni si trovano nella cartella delle librerie SCF:

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

Esempio:

* Nodo cartella client: `/libs/social/forum/hbs/forum/clientlibs`
* Proprietà Categorie: `cq.social.author.hbs.forum`

Nota: anche se le librerie client di authoring non incorporano mai altre librerie, elencano le loro dipendenze. Quando vengono incorporate in altre librerie, le dipendenze non vengono estratte automaticamente e devono essere incorporate.

Le clientlibs di authoring richieste possono essere identificate inserendo &quot;author&quot; nelle clientlibs elencate per ogni componente SCF nel [Guida ai componenti della community](components-guide.md).

### Considerazioni sull’utilizzo {#usage-considerations}

Ogni sito è diverso nelle modalità di gestione delle librerie client. Vari fattori includono:

* Velocità complessiva: Forse il desiderio è che il sito sia reattivo, ma è accettabile che la prima pagina sia un po&#39; lenta da caricare. Se molte pagine utilizzano lo stesso JavaScript, i vari Javascript possono essere incorporati in un clientlib e citati dalla prima pagina da caricare. Il codice JavaScript in questo singolo download rimane memorizzato nella cache, riducendo al minimo la quantità di dati da scaricare per le pagine successive.
* Tempo breve per la prima pagina: Forse il desiderio è che la prima pagina si carichi rapidamente. In questo caso, il codice Javascript si trova in più file di piccole dimensioni a cui fare riferimento solo laddove necessario.
* Un equilibrio tra il primo caricamento della pagina e i successivi download.

| **[⇐ funzioni di base](essentials.md)** | **[Informazioni sulla personalizzazione lato server](server-customize.md)** |
|---|---|
|  | **[Helpers Handlebars SCF](handlebars-helpers.md)** |
