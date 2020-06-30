---
title: Personalizzazione lato client
seo-title: Personalizzazione lato client
description: Personalizzazione del comportamento o dell'aspetto lato client negli AEM Communities
seo-description: Personalizzazione del comportamento o dell'aspetto lato client negli AEM Communities
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
translation-type: tm+mt
source-git-commit: efa6c7be93908b2f264da4689caa9c02912c0f0a
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 0%

---


# Personalizzazione lato client  {#client-side-customization}

| **[⇐ Funzioni Essenziali](essentials.md)** | **[Personalizzazione lato server ⇒](server-customize.md)** |
|---|---|
|  | **[Helper manubrio SCF](handlebars-helpers.md)** |

Per personalizzare l’aspetto e/o il comportamento di un componente AEM Communities sul lato client, sono disponibili diversi approcci.

Due approcci principali consistono nel sovrapporre o estendere un componente.

[La sovrapposizione](#overlays) di un componente modifica il componente predefinito e influenza ogni riferimento al componente.

[L’estensione](#extensions) di un componente con un nome univoco limita l’ambito delle modifiche. Il termine &#39;extension&#39; viene utilizzato in modo intercambiabile con &#39;override&#39;.

## Sovrapposizioni {#overlays}

La sovrapposizione di un componente è un metodo per apportare modifiche a un componente predefinito e per interessare tutte le istanze che utilizzano il componente predefinito.

La sovrapposizione viene realizzata modificando una copia del componente predefinito nella directory /**apps** , anziché modificare il componente originale nella directory /**libs** . Il componente è costruito con un percorso relativo identico, eccetto &#39;libs&#39; viene sostituito con &#39;apps&#39;.

La directory /apps è il primo posto in cui è stata eseguita la ricerca per risolvere le richieste e, se non viene trovata, viene utilizzata la versione predefinita presente nella directory /libs.

Il componente predefinito nella directory /libs non deve mai essere modificato in quanto le patch e gli aggiornamenti futuri sono liberi di modificare la directory /libs in qualsiasi modo necessario pur mantenendo le interfacce pubbliche.

Ciò è diverso dall’ [estensione](#extensions) di un componente predefinito in cui si desidera apportare modifiche per un uso specifico, la creazione di un percorso univoco per il componente e l’utilizzo di un riferimento al componente predefinito originale nella directory /libs come tipo di risorsa super.

Per un rapido esempio di sovrapposizione del componente commenti, provate l’esercitazione [sul componente](overlay-comments.md)Overlay Comments (Commenti sovrapposizione).

## Estensioni {#extensions}

L’estensione (esclusione) di un componente è un metodo per apportare modifiche per un uso specifico senza influire su tutte le istanze che utilizzano l’impostazione predefinita. Il componente esteso ha un nome univoco nella cartella /apps e fa riferimento al componente predefinito nella cartella /libs, pertanto la progettazione e il comportamento predefiniti di un componente non vengono modificati.

Ciò è diverso dalla [sovrapposizione](#overlays) del componente predefinito in cui la natura di Sling risolve i riferimenti relativi alle app/cartella prima di effettuare ricerche nella cartella libs/, pertanto la progettazione o il comportamento di un componente vengono modificati a livello globale.

Per un esempio rapido di estensione del componente commenti, provate l’esercitazione [](extend-comments.md)Estendi componente commenti.

## Binding Javascript {#javascript-binding}

Lo script HBS per il componente deve essere associato agli oggetti, ai modelli e alle viste JavaScript che implementano questa funzione.

Il valore dell&#39; `data-scf-component` attributo può essere il componente predefinito, ad esempio **`social/tally/components/hbs/rating`** o esteso (personalizzato) per funzionalità personalizzate, ad esempio **weretail/components/hbs/rating**.

Per eseguire un binding di un componente, l&#39;intero script del componente deve essere racchiuso all&#39;interno di un elemento &lt;div> con i seguenti attributi:

* `data-component-id`=&quot;{{id}}&quot;

   risolve la proprietà id dal contesto

* `data-scf-component`=&quot;*&lt;resourceType>*

Ad esempio, da `/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="{{id}}" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## Proprietà personalizzate {#custom-properties}

Quando si estende o si sovrappone un componente, è possibile aggiungere proprietà a una finestra di dialogo modificata.

Per accedere a tutte le proprietà impostate su un componente/risorsa, fare riferimento alle chiavi di proprietà nel modello handlebars:

`{{properties.<property_name>}}`

## Skin CSS {#skinning-css}

La personalizzazione dei componenti in base al tema generale del sito Web può essere ottenuta mediante la &quot;creazione di interfacce&quot;: modifica di colori, font, immagini, pulsanti, collegamenti, spaziatura e persino posizionamento in una certa misura.

La creazione di interfacce può essere ottenuta sostituendo selettivamente gli stili del framework o scrivendo fogli di stile completamente nuovi. I componenti SCF definiscono classi CSS con spazi di nomi, modulari e semantici che influiscono sui vari elementi che costituiscono un componente.

Per applicare uno skin a un componente:

1. Identificare gli elementi che si desidera modificare (ad esempio, area del compositore, pulsanti della barra degli strumenti, font del messaggio e così via).
1. Identificate le classi/regole CSS che influiscono su questi elementi.
1. Creare un file foglio di stile (.css).
1. Includete il foglio di stile in una cartella libreria client ([clientlibs](#clientlibs-for-scf)) per il sito e accertatevi che sia incluso nei modelli e nelle pagine con [ui:includeClientLib](../../help/sites-developing/clientlibs.md).

1. Ridefinire le classi e le regole CSS identificate (#2) nel foglio di stile e aggiungere stili.

Gli stili personalizzati sostituiranno gli stili framework predefiniti e il componente verrà rappresentato con il nuovo interfaccia.

>[!CAUTION]
>
>Qualsiasi nome di classe CSS con il prefisso `scf-js` ha un uso specifico nel codice javascript. Queste classi influiscono sullo stato di un componente (ad esempio, per passare da nascosto a visibile) e non devono essere né ignorate né rimosse.
>
>Anche se le `scf-js` classi non influiscono sugli stili, i nomi delle classi possono essere utilizzati in fogli di stile con l&#39;avvertenza che, mentre controllano gli stati degli elementi, ci possono essere effetti collaterali.


## Estensione di Javascript {#extending-javascript}

Per estendere un’implementazione Javascript per componenti, è necessario:

1. Create un componente per l’app con un jcr:resourceSuperType impostato sul valore del jcr:resourceType del componente esteso, ad esempio social/forum/components/hbs/forum.
1. Esaminate il codice JavaScript predefinito del componente SCF per determinare quali metodi devono essere registrati utilizzando SCF.registerComponent().
1. Copiate il codice JavaScript del componente esteso o iniziate da zero.
1. Estende il metodo.
1. Utilizzate SCF.registerComponent() per registrare tutti i metodi con le impostazioni predefinite o con gli oggetti e le viste personalizzati.

### forum.js: Esempio di estensione del forum - HBS  {#forum-js-sample-extension-of-forum-hbs}

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

I tag script sono parte integrante del framework lato client. Sono la combinazione che consente di associare la marcatura generata sul lato server ai modelli e alle viste sul lato client.

I tag script negli script SCF non devono essere rimossi quando si sovrappongono o si ignorano i componenti. I tag script SCF creati automaticamente per l&#39;invio di JSON nell&#39;HTML sono identificati con l&#39;attributo `data-scf-json=true`.

## Clientlibs per SCF {#clientlibs-for-scf}

L&#39;utilizzo di librerie [lato](../../help/sites-developing/clientlibs.md) client (clientlibs) consente di organizzare e ottimizzare i file Javascript e CSS utilizzati per il rendering del contenuto sul client.

I clientlibs per SCF seguono un pattern di denominazione molto specifico per due varianti, che varia solo in base alla presenza di &quot;author&quot; nel nome della categoria:

| Clientlib Variant | Pattern per la proprietà Categories |
|--- |--- |
| clientlib complete | cq.social.hbs.&lt;nome componente> |
| clientlib autore | cq.social.author.hbs.&lt;nome componente> |

### Clientlibs completi {#complete-clientlibs}

I clientlibs completi (non autori) includono dipendenze e sono utili per l&#39;inclusione con ui:includeClientLib.

Queste versioni sono disponibili in:

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

Ad esempio:

* Nodo cartella client: `/etc/clientlibs/social/hbs/forum`
* Proprietà Categories: `cq.social.hbs.forum`

La guida [Componenti](components-guide.md) community elenca tutti i clientlibs richiesti per ciascun componente SCF.

[Clientlibs for Communities Components](clientlibs.md) descrive come aggiungere clientlibs a una pagina.

### Autori Clientlibs {#author-clientlibs}

I clientlibs della versione dell’autore vengono ridotti al codice JavaScript minimo necessario per implementare il componente.

Questi clientlibs non dovrebbero mai essere inclusi direttamente, ma sono invece disponibili per incorporare altri clientlibs, creati a mano per un sito.

Queste versioni si trovano nella cartella delle librerie SCF:

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

Ad esempio:

* Nodo cartella client: `/libs/social/forum/hbs/forum/clientlibs`
* Proprietà Categories: `cq.social.author.hbs.forum`

Nota: mentre i clientlibs di autori non incorporano mai altre librerie, elencano comunque le rispettive dipendenze. Se incorporate in altre librerie, le dipendenze non vengono inserite automaticamente e devono essere incorporate.

I clientlibs di autori richiesti possono essere identificati inserendo &quot;author&quot; nei clientlibs elencati per ciascun componente SCF nella guida [Componenti](components-guide.md)community.

### Considerazioni sull&#39;utilizzo {#usage-considerations}

Ogni sito è diverso nella gestione delle librerie client. Diversi fattori includono:

* Velocità complessiva: Forse il desiderio è che il sito sia reattivo, ma è accettabile che la prima pagina sia un po &#39;lenta a caricarsi. Se molte delle pagine utilizzano lo stesso JavaScript, i vari Javascript possono essere incorporati in una clientlib e citati dalla prima pagina da caricare. Il codice JavaScript in questo singolo download rimane memorizzato nella cache, riducendo al minimo la quantità di dati da scaricare per le pagine successive.
* Tempo breve per la prima pagina: Forse il desiderio è che la prima pagina si carichi velocemente. In questo caso, Javascript si trova in più file di piccole dimensioni a cui verrà fatto riferimento solo se necessario.
* Un compromesso tra il caricamento della prima pagina e i successivi download.

| **[⇐ Funzioni Essenziali](essentials.md)** | **[Personalizzazione lato server ⇒](server-customize.md)** |
|---|---|
|  | **[Helper manubrio SCF](handlebars-helpers.md)** |

