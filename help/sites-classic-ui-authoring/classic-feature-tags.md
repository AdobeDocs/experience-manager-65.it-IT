---
title: Utilizzo dei tag
seo-title: Utilizzo dei tag
description: I tag sono un metodo semplice e veloce per classificare i contenuti di un sito web. I tag possono essere paragonati a parole chiave o etichette assegnate a una pagina, una risorsa o ad altro contenuto per consentire la ricerca di contenuti specifici e correlati.
seo-description: I tag sono un metodo semplice e veloce per classificare i contenuti di un sito web. I tag possono essere paragonati a parole chiave o etichette assegnate a una pagina, una risorsa o ad altro contenuto per consentire la ricerca di contenuti specifici e correlati.
uuid: 9799131f-4043-4022-a401-af8be93a1bf6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: c117b9d1-e4ae-403f-8619-6e48d424a761
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4

---


# Utilizzo dei tag{#using-tags}

I tag sono un metodo semplice e veloce per classificare i contenuti di un sito web. I tag possono essere paragonati a parole chiave o etichette assegnate a una pagina, una risorsa o ad altro contenuto per consentire la ricerca di contenuti specifici e correlati.

* See [Administering Tags](/help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.
* See [Tagging for Developers](/help/sites-developing/tags.md) for information about the tagging framework as well as including and extending tags in custom applications.

## Dieci motivi per utilizzare i tag {#ten-reasons-to-use-tagging}

1. Organizzazione dei contenuti: l’assegnazione di tag semplifica il lavoro agli autori, che possono organizzare rapidamente i contenuti con il minimo sforzo.
1. Organizzazione dei tag: i tag organizzano i contenuti, e le tassonomie (o namespace) gerarchiche organizzano i tag.
1. Tag estremamente organizzati: attraverso la creazione di tag principali e secondari, è possibile creare tassonomie complete che includono termini, termini derivati e relazioni che li collegano. Questo permette di creare una seconda (o terza) gerarchia di contenuti parallela a quella ufficiale.
1. Tagging controllato: l’aggiunta di tag può essere controllata applicando autorizzazioni ai tag e/o ai namespace per controllare la creazione e l’applicazione di tag.
1. Tagging flessibile: i tag possono avere molti nomi diversi, come tag, termini di tassonomia, categorie, etichette e molto altro ancora. Sono flessibili dal punto di vista di modello di contenuto e modalità di utilizzo. Possono essere ad esempio utilizzati per sintetizzare le caratteristiche demografiche del target, suddividere in categorie e classificare i contenuti o creare una gerarchia di contenuti secondaria.
1. Ricerca migliorata: il componente di ricerca predefinito in AEM include i tag creati e assegnati a cui possono essere applicati filtri per restringere i risultati a quelli rilevanti.
1. Abilitazione SEO: i tag assegnati come proprietà della pagina vengono visualizzati automaticamente nei metatag della pagina, rendendola visibile ai motori di ricerca.
1. Sofisticazione semplice: i tag possono essere creati da una parola e dal tocco di un pulsante. In seguito, è possibile aggiungere un titolo, una descrizione ed etichette illimitate per fornire ulteriore semantica al tag.
1. Coerenza di base: il sistema di tagging è un componente di base di AEM ed è utilizzato da tutte le funzioni AEM per classificare i contenuti. Inoltre, l’API di tagging è disponibile agli sviluppatori per creare applicazioni abilitate ai tag con accesso alle stesse tassonomie.
1. Struttura e flessibilità: AEM è ideale per lavorare con informazioni strutturate, grazie alla nidificazione delle pagine e dei percorsi. È molto efficace anche per la gestione delle informazioni non strutturate, grazie alla funzione integrata di ricerca testuale. L’assegnazione di tag offre i vantaggi delle struttura e della flessibilità.

Quando progetti la struttura dei contenuti di un sito e lo schema di metadati per le risorse, considera l’approccio leggero e accessibile fornito dai tag.

## Applicazione dei tag {#applying-tags}

In the author environment, authors may apply tags by accessing the page properties and entering one or more tags in the **Tags/Keywords** field.

To apply [pre-defined tags](/help/sites-administering/tags.md), in the **Page Properties** window use the `Tags/Keywords` field pull-down to select from the list of tags permitted for the page. Tthe **Standard Tags** tab is the default namespace, which means there is no `namespace-string:` prefixed to the taxonomy.

![chlimage_1-2](assets/chlimage_1-2a.png)

### Pubblicazione dei tag {#publishing-tags}

Come avviene per le pagine, su tag e namespace è possibile effettuare le operazioni descritte di seguito.

**Attiva**

* Consente di attivare singoli tag.

   Come per le pagine, i nuovi tag creati devono essere attivati per poter essere disponibili nell’ambiente di pubblicazione.

>[!NOTE]
>
>Quando si attiva una pagina, si apre automaticamente una finestra di dialogo che consente di attivare i tag non attivati appartenenti alla pagina.

**Disattiva**

* È possibile disattivare i tag selezionati.

## Tag cloud {#tag-clouds}

I tag cloud mostrano un insieme di tag relativi alla pagina corrente, all’intero sito Web o ai contenuti maggiormente utilizzati. I tag cloud sono uno strumento per evidenziare i problemi che sono (sono stati) di interesse per l’utente. Le dimensioni del testo utilizzato per visualizzare il tag variano a seconda dell&#39;uso.

Il componente [Tag cloud](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md#tag-cloud) (gruppo di componenti Generale) viene utilizzato per aggiungere un Tag cloud a una pagina.

## Ricerca sui tag {#searching-on-tags}

Puoi ricercare i tag sia nell’ambiente di creazione e modifica che nell’ambiente di pubblicazione.

### Uso del componente Ricerca {#using-search-component}

Adding a [Search component](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md#search) to a page provides a search capability which includes tags and can be used in both the author and publish environments.

![chlimage_1-3](assets/chlimage_1-3a.png)

