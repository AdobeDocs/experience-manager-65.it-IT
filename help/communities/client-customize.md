---
title: Personalizzazione lato client
description: Personalizzazione del comportamento o dell’aspetto lato client in AEM Communities
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: bf34f564-ac93-4c8c-95f7-8690d99d85cb
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 0%

---

# Personalizzazione lato client  {#client-side-customization}

| **[⇐ caratteristiche di base](essentials.md)** | **[Personalizzazione lato server ⇒](server-customize.md)** |
|---|---|
|   | **[Helper Handlebars SCF ⇒](handlebars-helpers.md)** |

Per personalizzare l’aspetto e/o il comportamento di un componente AEM Communities sul lato client, esistono diversi approcci.

Due approcci principali sono la sovrapposizione o l’estensione di un componente.

[Sovrapposizione](#overlays) di un componente cambia il componente predefinito e influisce su ogni riferimento al componente.

[L&#39;estensione](#extensions) di un componente, con un nome univoco, limita l&#39;ambito delle modifiche. Il termine &#39;extend&#39; viene usato in modo intercambiabile con &#39;override&#39;.

## Sovrapposizioni {#overlays}

La sovrapposizione di un componente è un metodo che consente di apportare modifiche a un componente di default e di influire su tutte le varianti che lo utilizzano.

La sovrapposizione viene eseguita modificando una copia del componente predefinito nella directory /**apps**, anziché modificando il componente originale nella directory /**libs**. Il componente è costruito con un percorso relativo identico, ad eccezione di &#39;libs&#39; che viene sostituito con &#39;apps&#39;.

La directory /apps è la prima posizione in cui viene eseguita la ricerca per risolvere le richieste e, se non viene trovata, viene utilizzata la versione predefinita nella directory/libs.

Il componente predefinito nella directory /libs non deve mai essere modificato in quanto le patch e gli aggiornamenti futuri sono liberi di modificare la directory /libs in qualsiasi modo necessario mantenendo le interfacce pubbliche.

Questo è diverso da [extension](#extensions) un componente predefinito in cui si desidera apportare modifiche per un uso specifico, creando un percorso univoco al componente e facendo riferimento al componente predefinito originale nella directory /libs come tipo di risorsa super.

Per un rapido esempio di sovrapposizione del componente Commenti, prova l&#39;esercitazione [Componente Commenti sovrapposti](overlay-comments.md).

## Estensioni {#extensions}

L’estensione (esclusione) di un componente è un metodo per apportare modifiche per un uso specifico senza influire su tutte le istanze che utilizzano l’impostazione predefinita. Il componente esteso ha un nome univoco nella cartella /apps e fa riferimento al componente predefinito nella cartella /libs, pertanto la progettazione e il comportamento predefiniti di un componente non vengono modificati.

Questo è diverso da [sovrapposizione](#overlays) del componente predefinito in cui la natura di Sling risolve i riferimenti relativi alla cartella apps/ prima di effettuare la ricerca nella cartella libs/, pertanto la progettazione o il comportamento di un componente viene modificato a livello globale.

Per un rapido esempio di estensione del componente Commenti, prova l&#39;esercitazione [Estendi componente Commenti](extend-comments.md).

## Binding JavaScript {#javascript-binding}

Lo script HBS per il componente deve essere associato agli oggetti, ai modelli e alle viste di JavaScript che implementano questa funzione.

Il valore dell&#39;attributo `data-scf-component` può essere il valore predefinito, ad esempio **`social/tally/components/hbs/rating`**, o un componente esteso (personalizzato) per funzionalità personalizzate, ad esempio **weretail/components/hbs/rating**.

Per associare un componente, l’intero script del componente deve essere racchiuso in un elemento &lt;div> con i seguenti attributi:

* `data-component-id`=&quot;`{{id}}`&quot;

  viene risolto nella proprietà id dal contesto

* `data-scf-component`=&quot;*&lt;tipoRisorsa>*

Ad esempio, da `/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="`{{id}}`" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## Proprietà personalizzate {#custom-properties}

Quando si estende o si sovrappone un componente, è possibile aggiungere proprietà a una finestra di dialogo modificata.

È possibile accedere a tutte le proprietà impostate su un componente o una risorsa facendo riferimento alle chiavi di proprietà nel modello Handlebars:

`{{properties.<property_name>}}`

## CSS interfaccia {#skinning-css}

Personalizzare i componenti in modo che corrispondano al tema generale del sito web può essere ottenuto &quot;scuoiando&quot;: cambiando colori, font, immagini, pulsanti, collegamenti, spaziatura e persino posizionando in una certa misura.

È possibile eseguire lo skin sostituendo in modo selettivo gli stili del framework o scrivendo fogli di stile completamente nuovi. I componenti SCF definiscono classi CSS con spazio dei nomi, modulari e semantiche che influiscono sui vari elementi che compongono un componente.

Per applicare lo skin a un componente:

1. Identificare gli elementi che si desidera modificare (ad esempio l&#39;area del compositore, i pulsanti della barra degli strumenti, il carattere del messaggio e così via).
1. Identifica la classe CSS o le regole che influenzano questi elementi.
1. Creare un file del foglio di stile (css).
1. Includi il foglio di stile in una cartella della libreria client ([clientlibs](#clientlibs-for-scf)) per il tuo sito e assicurati che sia incluso nei modelli e nelle pagine con [ui:includeClientLib](../../help/sites-developing/clientlibs.md).

1. Ridefinire le classi e le regole CSS identificate (#2) nel foglio di stile e aggiungere stili.

Gli stili personalizzati sovrascriveranno gli stili di framework predefiniti e il componente verrà renderizzato con il nuovo skin.

>[!CAUTION]
>
>Qualsiasi nome di classe CSS con prefisso `scf-js` ha un utilizzo specifico nel codice JavaScript. Queste classi influiscono sullo stato di un componente (ad esempio, da nascosto a visibile) e non devono essere ignorate né rimosse.
>
>Anche se le classi `scf-js` non influiscono sugli stili, i nomi delle classi possono essere utilizzati nei fogli di stile con l&#39;avvertenza che, poiché controllano gli stati degli elementi, potrebbero verificarsi effetti collaterali.

## Estensione di JavaScript {#extending-javascript}

Per estendere un’implementazione di JavaScript per componenti, è necessario:

1. Crea un componente per la tua app con un jcr:resourceSuperType impostato sul valore del jcr:resourceType del componente esteso, ad esempio social/forum/components/hbs/forum.
1. Esaminate il JavaScript del componente SCF predefinito per determinare quali metodi devono essere registrati utilizzando SCF.registerComponent().
1. Copia il JavaScript del componente esteso o inizia da zero.
1. Estendere il metodo.
1. Utilizzare SCF.registerComponent() per registrare tutti i metodi con le impostazioni predefinite o con gli oggetti e le visualizzazioni personalizzate.

### forum.js: esempio di estensione del forum - HBS  {#forum-js-sample-extension-of-forum-hbs}

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

I tag script sono parte integrante del framework lato client. Sono l’associazione che consente di associare il markup generato sul lato server ai modelli e alle viste sul lato client.

I tag di script negli script SCF non devono essere rimossi quando si sovrappongono o si sovrascrivono i componenti. I tag script SCF creati automaticamente per l&#39;inserimento di JSON nel HTML sono identificati con l&#39;attributo `data-scf-json=true`.

## Clientlibs per SCF {#clientlibs-for-scf}

L&#39;utilizzo di [librerie lato client](../../help/sites-developing/clientlibs.md) (clientlibs) consente di organizzare e ottimizzare il JavaScript e i CSS utilizzati per il rendering del contenuto sul client.

Le clientlibs per SCF seguono un pattern di denominazione molto specifico per due varianti, che varia solo in base alla presenza di &quot;author&quot; nel nome della categoria:

| Variante Clientlib | Pattern per proprietà Categories |
|--- |--- |
| clientlib completa | cq.social.hbs.&lt;nome componente> |
| author clientlib | cq.social.author.hbs.&lt;nome componente> |

### Clientlibs complete {#complete-clientlibs}

Le clientlibs complete (non di authoring) includono dipendenze e sono comode da includere con ui:includeClientLib.

Queste versioni si trovano in:

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

Ad esempio:

* Nodo cartella client: `/etc/clientlibs/social/hbs/forum`
* Proprietà Categories: `cq.social.hbs.forum`

Nella [guida ai componenti community](components-guide.md) sono elencate le clientlibs complete necessarie per ogni componente SCF.

[Clientlibs per i componenti Communities](clientlibs.md) descrive come aggiungere clientlibs a una pagina.

### Creatore Clientlibs {#author-clientlibs}

Le clientlibs della versione di authoring vengono ridotte al minimo JavaScript necessario per implementare il componente.

Queste clientlibs non devono mai essere incluse direttamente, ma sono disponibili per l’incorporamento in altre clientlibs, create a mano per un sito.

Queste versioni si trovano nella cartella SCF libs:

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

Ad esempio:

* Nodo cartella client: `/libs/social/forum/hbs/forum/clientlibs`
* Proprietà Categories: `cq.social.author.hbs.forum`

Nota: anche se author clientlibs non incorpora mai altre librerie, elenca effettivamente le loro dipendenze. Quando sono incorporate in altre librerie, le dipendenze non vengono inserite automaticamente e devono essere incorporate.

Le clientlibs di authoring richieste possono essere identificate inserendo &quot;author&quot; nelle clientlibs elencate per ciascun componente SCF nella [guida dei componenti community](components-guide.md).

### Considerazioni sull’utilizzo {#usage-considerations}

Ogni sito è diverso nel modo in cui gestisce le librerie client. Vari fattori includono:

* Velocità complessiva: forse il desiderio è che il sito sia reattivo, ma è accettabile che la prima pagina sia un po&#39; lenta da caricare. Se molte pagine utilizzano lo stesso JavaScript, è possibile incorporare i vari JavaScript in una libreria client e farvi riferimento dalla prima pagina da caricare. Il JavaScript in questo singolo download rimane memorizzato nella cache, riducendo al minimo la quantità di dati da scaricare per le pagine successive.
* Breve tempo alla prima pagina: forse il desiderio è che la prima pagina venga caricata rapidamente. In questo caso, il JavaScript si trova in più file di piccole dimensioni a cui fare riferimento solo quando necessario.
* Equilibrio tra il primo caricamento della pagina e i download successivi.

| **[⇐ caratteristiche di base](essentials.md)** | **[Personalizzazione lato server ⇒](server-customize.md)** |
|---|---|
|   | **[Helper Handlebars SCF ⇒](handlebars-helpers.md)** |
