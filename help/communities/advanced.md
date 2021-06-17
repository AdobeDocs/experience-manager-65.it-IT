---
title: Punteggio e badge avanzati
seo-title: Punteggio e badge avanzati
description: Impostazione del punteggio avanzato
seo-description: Impostazione del punteggio avanzato
uuid: 48caca57-43d3-4f2f-adf3-257428ba54d5
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: eb3d5c37-8097-46de-8c4f-804ea723f1c5
docset: aem65
role: Administrator
exl-id: d3bb6664-6c01-4bcf-840c-072fc491fc99
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---

# Punteggio e badge avanzati{#advanced-scoring-and-badges}

## Panoramica {#overview}

Il punteggio avanzato consente di assegnare i badge per identificare i membri come esperti. Il punteggio avanzato assegna i punti in base alla quantità *e* di contenuto creato da un membro, mentre il punteggio di base assegna i punti semplicemente in base alla quantità di contenuto creato.

Questa differenza è dovuta al motore di valutazione utilizzato per calcolare i punteggi. Il motore di punteggio di base applica una matematica semplice. Il motore di valutazione avanzato è un algoritmo adattivo che premia i membri attivi che contribuiscono a contenuti importanti e valutati, detratti attraverso l’elaborazione delle lingue naturali (NLP) di un argomento.

Oltre alla rilevanza del contenuto, gli algoritmi di punteggio tengono conto delle attività dei membri, come il voto e la percentuale di risposte. Il punteggio di base li include in termini quantitativi, mentre il punteggio avanzato li utilizza in modo algoritmico.

Pertanto, il motore di valutazione avanzato richiede dati sufficienti per rendere significativa l’analisi. La soglia di successo per diventare un esperto viene costantemente rivalutata in quanto l&#39;algoritmo si regola continuamente sul volume e la qualità dei contenuti creati. C&#39;è anche un concetto di *decadimento* dei post precedenti di un membro. Se un membro esperto smette di partecipare all&#39;oggetto in cui ha ottenuto lo status di esperto, ad un certo punto predeterminato (vedere [configurazione del motore di punteggio](#configurable-scoring-engine)) potrebbe perdere il proprio status di esperto.

L’impostazione del punteggio avanzato è praticamente identica al punteggio di base:

* Le regole di valutazione e contrassegno di base e avanzate sono [applicate al contenuto](/help/communities/implementing-scoring.md#apply-rules-to-content) nello stesso modo.

   * Le regole di valutazione e contrassegno di base e avanzate possono essere applicate allo stesso contenuto.

* [Abilitazione dei badge per i ](/help/communities/implementing-scoring.md#enable-badges-for-component) componenti generici.

Le differenze nella configurazione delle regole di valutazione e di badging sono le seguenti:

* Motore di valutazione avanzato configurabile
* Regole di valutazione avanzate:

   * `scoringType` impostato su  `advanced`
   * Richiede `stopwords`

* Regole di contrassegno avanzate:

   * `badgingType` impostato su  `advanced`
   * `badgingLevels` è fissato al  **numero di livelli di esperti da assegnare**
   * Richiede una matrice `badgingPaths` di badge invece delle soglie dei punti di mappatura degli array sui badge.

>[!NOTE]
>
>Per utilizzare le funzionalità avanzate di valutazione e contrassegno, installa il [pacchetto di identificazione esperto](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/social/cq-social-expert-identification-pkg).

## Motore di valutazione configurabile {#configurable-scoring-engine}

Il motore di punteggio avanzato fornisce una configurazione OSGi con parametri che influiscono sull’algoritmo di punteggio avanzato.

![motore a punteggio avanzato](assets/advanced-scoring-engine.png)

* **Pesi del punteggio**

   Per un argomento, specifica il verbo a cui deve essere data la priorità più alta durante il calcolo del punteggio. È possibile inserire uno o più argomenti, ma è limitato a **un verbo per argomento**. Vedere [Argomenti e verbi](/help/communities/implementing-scoring.md#topics-and-verbs).
Inserito come `topic,verb` con la virgola in sequenza. Esempio:
   `/social/forum/hbs/social/forum\,ADD`
L’impostazione predefinita è impostata sul verbo ADD per i componenti QnA e forum.

* **Intervallo di valutazione**

   L’intervallo per i punteggi avanzati è definito da questo valore (punteggio massimo possibile) e da 0 (punteggio più basso possibile).

   Il valore predefinito è 100, quindi l’intervallo di punteggio è compreso tra 0 e 100.

* **Intervallo di tempo decadimento entità**

   Questo parametro rappresenta il numero di ore in cui tutti i punteggi dell’entità sono decaduti. Questo è necessario per non includere più i vecchi contenuti nei punteggi di un sito community.

   Il valore predefinito è 216000 ore (~24 anni).

* **Punteggio del**
tasso di crescitaQuesto specifica il punteggio tra 0 e la fascia di punteggio, oltre il quale la crescita rallenta per limitare il numero di esperti.

   Il valore predefinito è 50.

## Regole di valutazione avanzate {#advanced-scoring-rules}

Nel punteggio di base, è nota la quantità necessaria per ottenere un badge.

Nel punteggio avanzato, la quantità necessaria viene costantemente adattata in base alla quantità di dati di qualità all&#39;interno del sistema. Il punteggio viene continuamente calcolato in modo simile a una curva a campana.

Se un membro ha guadagnato un badge esperto su un argomento che non è più attivo, c&#39;è la possibilità che perderà il loro badge a causa di decadimento nel tempo.

### scoringType {#scoringtype}

Una regola di punteggio è un insieme di regole secondarie di punteggio, ciascuna delle quali dichiara il valore `scoringType`.

Per richiamare il motore di punteggio avanzato, è necessario impostare `scoringType`su `advanced`.

Consulta [Sottoregole di punteggio](/help/communities/implementing-scoring.md#scoring-sub-rules).

![tipo avanzato di punteggio](assets/advanced-scoring-type.png)

### Punte {#stopwords}

Il pacchetto di valutazione avanzato installa una cartella di configurazione contenente un file di parole chiave:

* `/libs/settings/community/scoring/configuration/stopwords`

L’algoritmo di valutazione avanzato utilizza l’elenco di parole contenute nel file stopwords per identificare le parole inglesi comuni che vengono ignorate durante l’elaborazione del contenuto.

Non è previsto che il file venga modificato.

Se il file delle parole chiave è mancante, il motore di punteggio avanzato genererà un errore.

## Regole di contrassegno avanzate {#advanced-badging-rules}

Le proprietà avanzate della regola di badging sono diverse dalle proprietà [base della regola di badging](/help/communities/implementing-scoring.md#badging-rules).

Invece di associare i punti a un’immagine del badge, è necessario solo identificare il numero di esperti consentiti e l’immagine del badge da assegnare.

![regole avanzate di badging](assets/advanced-badging-rules.png)

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Tipo</th>
   <th>Valore Descrizione</th>
  </tr>
  <tr>
   <td>badgingPath</td>
   <td>Stringa[]</td>
   <td><em>(Obbligatorio)</em> Una stringa con più valori di immagini di badge fino al numero di badgingLevels. I percorsi immagine del badge devono essere ordinati in modo che il primo venga assegnato all’esperto più alto. Se sono presenti meno badge rispetto a quelli indicati da badgingLevels, l’ultimo badge nell’array riempie il resto dell’array. Esempio di voce:<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>Lungo</td>
   <td><em>(Facoltativo) </em> Specifica i livelli di esperienza da assegnare. Ad esempio, se ci devono essere un <code>expert </code>e un <code>almost expert</code> (due badge), il valore deve essere impostato su 2. Il badgingLevel deve corrispondere al numero di immagini del badge relative agli esperti elencate per la proprietà badgingPath . Il valore predefinito è 1.</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Stringa</td>
   <td><em>(Obbligatorio)</em> Identifica il motore di punteggio come "base" o "avanzato". Imposta su "advanced" altrimenti il valore predefinito è "basic".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Stringa[]</td>
   <td><em>(Facoltativo) </em> Una stringa con più valori per limitare la regola di contrassegno agli eventi di punteggio identificati dalle regole di punteggio elencate.<br /> Voce di esempio: <br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> Il valore predefinito non è una restrizione.</td>
  </tr>
 </tbody>
</table>

## Regole incluse e badge {#included-rules-and-badge}

### Badge incluso {#included-badge}

In questa versione beta è incluso un badge di esperti basato su premi:

* `expert`

   `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![tesserino](assets/included-badge.png)

Affinché il badge dell’esperto appaia come premio per l’attività, assicurati:

* `Badges` sono abilitate per la funzione , ad esempio un forum o un componente QnA .

* Le regole avanzate di valutazione e contrassegno vengono applicate alla pagina (o predecessore) in cui è posizionato il componente.

Consulta le informazioni di base per:

* [Abilitazione del contrassegno per un componente](/help/communities/implementing-scoring.md#enableforcomponent)
* [Applicazione delle regole](/help/communities/implementing-scoring.md#applytopage)

### Regole di punteggio e sottorete incluse {#included-scoring-rules-and-sub-rules}

Nella versione beta sono incluse due regole di punteggio avanzate per la [funzione forum](/help/communities/functions.md#forum-function) (una per ogni componente forum e commenti della funzione forum):

1. `/libs/settings/community/scoring/rules/adv-comments-scoring`

   ```
   subRules[] =
   /libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
   /libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
   /libs/settings/community/scoring/rules/sub-rules/adv-voting-rule
   ```

1. `/libs/settings/community/scoring/rules/adv-forums-scoring`

   ```
   subRules[] =
   /libs/settings/community/scoring/rules/sub-rules/adv-forums-rule
   /libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
   /libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
   ```

**Note:**

* I nodi `rules` e `sub-rules` sono entrambi di tipo `cq:Page`.
* `subRules` è un attributo di tipo Stringon `[]` the  `jcr:content` node della regola.
* `sub-rules` possono essere condivisi tra diverse regole di punteggio.
* `rules` devono trovarsi in una posizione archivio con autorizzazione di lettura per tutti.
* I nomi delle regole devono essere univoci indipendentemente dalla posizione.

### Regole di contrassegno incluse {#included-badging-rules}

Nella versione sono incluse due regole di badging avanzate che corrispondono ai [forum avanzati e regole di punteggio dei commenti](#included-scoring-rules-and-sub-rules).

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**Note:**

* `rules` i nodi sono di tipo cq:Page.
* `rules` devono trovarsi in una posizione archivio con autorizzazione di lettura per tutti.
* I nomi delle regole devono essere univoci indipendentemente dalla posizione.
