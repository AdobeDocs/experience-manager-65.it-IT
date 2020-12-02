---
title: 'Utilizzo dei tag  '
seo-title: 'Utilizzo dei tag  '
description: I tag sono un metodo semplice e veloce per classificare i contenuti di un sito web
seo-description: I tag sono un metodo semplice e veloce per classificare i contenuti di un sito web
uuid: 5d922443-f924-426e-acf4-27dffd1053f6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 9fb6d603-eb17-4192-bfa6-6c316f14ac7d
docset: aem65
translation-type: tm+mt
source-git-commit: 52cb99353ae33c8097b6b5bd29f6c040df30b42d
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 84%

---


# Utilizzo dei tag  {#using-tags}

I tag sono un metodo semplice e veloce per classificare i contenuti di un sito web. I tag possono essere paragonati a parole chiave o etichette assegnate a una pagina, una risorsa o ad altro contenuto per consentire la ricerca di contenuti specifici e correlati.

* Per informazioni sulla creazione e la gestione dei tag, nonché sui tag di contenuto applicati, consultate [Amministrazione dei tag](/help/sites-administering/tags.md).
* Per informazioni sul framework dei tag, nonché sull&#39;inclusione e l&#39;estensione dei tag nelle applicazioni personalizzate, consultate [Tagging per sviluppatori](/help/sites-developing/tags.md).

## Dieci motivi per utilizzare l’assegnazione tag {#ten-reasons-to-use-tagging}

1. **Organizzazione dei contenuti**: l’assegnazione tag semplifica il lavoro degli autori, che possono organizzare rapidamente i contenuti con il minimo sforzo.
1. **Organizzazione dei tag**: i tag consentono di organizzare contenuti, mentre le tassonomie o i namespace gerarchici consentono di organizzare i tag.
1. **Tag estremamente organizzati**: grazie all’assegnazione di tag principali e secondari, è possibile creare tassonomie complete che includono termini, termini derivati e relazioni che li collegano. In questo modo è possibile creare una seconda (o terza) gerarchia di contenuti parallela a quella ufficiale.
1. **Assegnazione tag controllata**: per gestire l’assegnazione tag, è possibile applicare autorizzazioni ai tag e/o ai namespace e controllare la creazione e l’applicazione di tag.
1. **Assegnazione tag flessibile**: i tag possono avere nomi diversi, come tag, termini di tassonomia, categorie, etichette e molto altro ancora. Sono flessibili dal punto di vista del modello di contenuto e della modalità di utilizzo. Possono essere ad esempio utilizzati per sintetizzare le caratteristiche demografiche del target, suddividere in categorie e classificare i contenuti o creare una gerarchia di contenuti secondaria.
1. **Ricerca migliorata**: il componente di ricerca predefinito in AEM include i tag creati e assegnati a cui possono essere applicati filtri per restringere i risultati solo a quelli pertinenti.
1. **Abilitazione SEO**: i tag applicati come proprietà della pagina vengono visualizzati automaticamente nei metatag della pagina, rendendola visibile ai motori di ricerca.
1. **Funzionalità sofisticate e al contempo semplici**: per creare i tag, basta selezionare una parola e fare clic su un pulsante. In seguito, è possibile aggiungere un titolo, una descrizione ed etichette illimitate per fornire ulteriore semantica al tag.
1. **Coerenza di base**: il sistema di assegnazione tag è un componente di base di AEM ed è utilizzato in tutte le funzioni AEM per la classificazione dei contenuti. Inoltre, per gli sviluppatori è disponibile l’API di assegnazione tag che consente di creare applicazioni abilitate per l’assegnazione tag con accesso alle stesse tassonomie.
1. **Struttura e flessibilità**: AEM è ideale per lavorare con informazioni strutturate, grazie alla nidificazione di pagine e percorsi. È molto efficace anche per la gestione delle informazioni non strutturate, grazie alla funzione integrata di ricerca testuale. L’assegnazione di tag offre i vantaggi delle struttura e della flessibilità.

Quando progetti la struttura dei contenuti di un sito e lo schema di metadati per le risorse, considera l’approccio leggero e accessibile fornito dai tag.

## Applicazione dei tag   {#applying-tags}

Nell’ambiente di authoring gli autori possono applicare i tag accedendo alle proprietà della pagina e immettendo uno o più tag nel campo **Tag/Parole chiave**.

Per applicare [tag predefiniti](/help/sites-administering/tags.md), nella finestra **Proprietà pagina** utilizzare il campo **Tag** e la finestra **Seleziona tag**. La scheda **Tag standard** è il namespace predefinito, il che significa che non esiste una `namespace-string:` aggiunta come prefisso alla tassonomia.

![Selezionare la finestra Tag; utilizzare il pulsante X per deselezionare i tag attualmente selezionati](assets/chlimage_1-41.png)

### Pubblicazione dei tag {#publishing-tags}

Come avviene per le pagine, su tag e namespace è possibile effettuare le operazioni descritte di seguito.

**Attiva**

* Consente di attivare singoli tag.

   Come per le pagine, è necessario attivare i nuovi tag creati prima che siano disponibili nell’ambiente di pubblicazione.

>[!NOTE]
>
>Quando si attiva una pagina, si apre automaticamente una finestra di dialogo che consente di attivare i tag non attivati appartenenti alla pagina.

**Disattiva**

* Consente di disattivare i tag selezionati.
