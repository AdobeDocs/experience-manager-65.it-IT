---
title: Punteggio e distintivi avanzati
seo-title: Punteggio e distintivi avanzati
description: Impostazione del punteggio avanzato
seo-description: Impostazione del punteggio avanzato
uuid: 48caca57-43d3-4f2f-adf3-257428ba54d5
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: eb3d5c37-8097-46de-8c4f-804ea723f1c5
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---


# Punteggio avanzato e distintivi{#advanced-scoring-and-badges}

## Panoramica {#overview}

Il punteggio avanzato consente di assegnare i distintivi per identificare i membri come esperti. Il punteggio avanzato assegna punti in base alla quantità di contenuto *e* creata da un membro, mentre il punteggio di base assegna punti semplicemente in base alla quantità di contenuto creata.

Questa differenza è dovuta al motore di valutazione utilizzato per calcolare i punteggi. Il motore di punteggio di base applica la matematica semplice. Il motore di valutazione avanzato è un algoritmo adattivo che premia i membri attivi che contribuiscono al contenuto con valore e rilevanza, dedotto attraverso l&#39;elaborazione in linguaggio naturale (NLP) di un argomento.

Oltre alla rilevanza del contenuto, gli algoritmi di punteggio tengono conto delle attività dei membri, come il voto e la percentuale di risposte. Mentre il punteggio di base li include in termini quantitativi, il punteggio avanzato li utilizza algoritmicamente.

Pertanto, il motore di valutazione avanzato richiede dati sufficienti per rendere significativa l&#39;analisi. La soglia di successo per diventare un esperto viene costantemente rivalutata man mano che l&#39;algoritmo si adatta continuamente al volume e alla qualità dei contenuti creati. Esiste anche un concetto di *decadimento* dei post precedenti di un membro. Se un membro esperto interrompe la partecipazione all&#39;argomento per il quale ha ottenuto lo status di esperto, ad un certo punto predeterminato (vedere [configurazione del motore di punteggio](#configurable-scoring-engine)) potrebbe perdere il proprio stato di esperto.

L’impostazione del punteggio avanzato è praticamente uguale al punteggio di base:

* Le regole di punteggio e contrassegno di base e avanzate sono [applicate al contenuto](/help/communities/implementing-scoring.md#apply-rules-to-content) nello stesso modo.

   * Le regole di punteggio e contrassegno di base e avanzate possono essere applicate allo stesso contenuto.

* [Abilitazione dei simboli per i ](/help/communities/implementing-scoring.md#enable-badges-for-component) componenti generici.

Le differenze nella configurazione delle regole di punteggio e contrassegno sono:

* Motore di valutazione avanzato configurabile
* Regole di punteggio avanzate:

   * `scoringType` impostato su  `advanced`
   * Richiede `stopwords`

* Regole di contrassegno avanzate:

   * `badgingType` impostato su  `advanced`
   * `badgingLevels` impostare il  **numero di livelli di esperti da assegnare**
   * Richiede `badgingPaths` array di simboli invece dei punti di mappatura della matrice delle soglie ai simboli.

>[!NOTE]
>
>Per utilizzare funzionalità avanzate di assegnazione dei punteggi e contrassegno, installare il [pacchetto di identificazione degli esperti](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/social/cq-social-expert-identification-pkg).

## Motore di punteggio configurabile {#configurable-scoring-engine}

Il motore di punteggio avanzato fornisce una configurazione OSGi con parametri che influiscono sull’algoritmo di punteggio avanzato.

![motore a punteggio avanzato](assets/advanced-scoring-engine.png)

* **Pesi punteggio**

   Per un argomento, specificate il verbo a cui assegnare la priorità più alta per il calcolo del punteggio. È possibile inserire uno o più argomenti, ma solo un verbo **per argomento**. Vedere [Argomenti e verbi](/help/communities/implementing-scoring.md#topics-and-verbs).
Inserito come `topic,verb` con la virgola con carattere di escape. Esempio:
   `/social/forum/hbs/social/forum\,ADD`
L’impostazione predefinita è impostata sul verbo ADD per i componenti QnA e forum.

* **Intervallo di punteggio**

   L’intervallo per i punteggi avanzati è definito da questo valore (valutazione massima possibile) e da 0 (valutazione più bassa possibile).

   Il valore predefinito è 100 e l’intervallo di punteggio è compreso tra 0 e 100.

* **Intervallo di tempo decadimento entità**

   Questo parametro rappresenta il numero di ore dopo le quali tutti i punteggi dell&#39;entità sono disattivati. Ciò non è più necessario per non includere contenuti obsoleti nelle valutazioni di un sito community.

   Il valore predefinito è 216000 ore (~24 anni).

* **Punteggio**
tasso di crescitaIndica il punteggio tra 0 e l&#39;intervallo di punteggio, oltre il quale la crescita rallenta per limitare il numero di esperti.

   Il valore predefinito è 50.

## Regole di punteggio avanzate {#advanced-scoring-rules}

Nel punteggio di base, è nota la quantità necessaria per ottenere un contrassegno.

Nel punteggio avanzato, la quantità necessaria viene costantemente regolata in base alla quantità di dati di qualità all&#39;interno del sistema. Il punteggio viene calcolato in modo continuativo in modo simile a una curva a campana.

Se un membro ha ottenuto un badge esperto su un argomento che non è più attivo, c&#39;è la possibilità che essi perderanno il loro badge a causa di decadimento nel tempo.

### scoringType {#scoringtype}

Una regola di punteggio è un insieme di regole secondarie di punteggio, ciascuna delle quali dichiara la `scoringType`.

Per richiamare il motore di punteggio avanzato, è necessario impostare `scoringType`su `advanced`.

Vedere [Regole secondarie di punteggio](/help/communities/implementing-scoring.md#scoring-sub-rules).

![di punteggio avanzato](assets/advanced-scoring-type.png)

### Stopwords {#stopwords}

Il pacchetto di punteggio avanzato installa una cartella di configurazione che contiene un file di parole di arresto:

* `/libs/settings/community/scoring/configuration/stopwords`

L&#39;algoritmo avanzato di valutazione utilizza l&#39;elenco di parole contenute nel file delle parole chiave per identificare le parole inglesi comuni che vengono ignorate durante l&#39;elaborazione del contenuto.

Non è previsto che il file venga modificato.

Se manca il file delle parole di arresto, il motore di punteggio avanzato genererà un errore.

## Regole di Badking avanzate {#advanced-badging-rules}

Le proprietà avanzate della regola di contrassegno sono diverse dalle proprietà [base della regola di contrassegno](/help/communities/implementing-scoring.md#badging-rules).

Invece di associare i punti a un’immagine badge, è necessario solo identificare il numero di esperti consentiti e l’immagine del contrassegno da assegnare.

![regole avanzate per il contrassegno](assets/advanced-badging-rules.png)

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
   <td><em>(Obbligatorio)</em> Una stringa di più valori di immagini contrassegno fino al numero di badgingLevels. I percorsi immagine del contrassegno devono essere ordinati in modo che il primo venga assegnato all’esperto più alto. Se sono presenti meno simboli di quelli indicati da badgingLevels, l'ultimo contrassegno nell'array riempie il resto dell'array. Voce di esempio:<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>Lungo</td>
   <td><em>(Facoltativo)</em> Specifica i livelli di esperienza da assegnare. Ad esempio, se devono essere presenti un <code>expert </code>e un <code>almost expert</code> (due simboli), il valore deve essere impostato su 2. L'oggetto badgingLevel deve corrispondere al numero di immagini del contrassegno relative agli esperti elencate per la proprietà badgingPath. Il valore predefinito è 1.</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Stringa</td>
   <td><em>(Obbligatorio)</em> Identifica il motore di valutazione come "base" o "avanzato". Impostato su "advanced", altrimenti il valore predefinito è "basic".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Stringa[]</td>
   <td><em>(Facoltativo)</em> Stringa con più valori per limitare la regola di contrassegno agli eventi di punteggio identificati dalle regole di punteggio elencate.<br /> Voce di esempio: <br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> il valore predefinito non è alcuna restrizione.</td>
  </tr>
 </tbody>
</table>

## Regole incluse e Badge {#included-rules-and-badge}

### Badge incluso {#included-badge}

In questa versione beta è incluso un badge di esperti basato sui premi:

* `expert`

   `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![tesserino](assets/included-badge.png)

Affinché il contrassegno dell&#39;esperto venga visualizzato come ricompensa per l&#39;attività, accertatevi che:

* `Badges` sono abilitate per la funzione, ad esempio un forum o un componente QnA.

* Le regole avanzate di valutazione e contrassegno vengono applicate alla pagina (o antenato) in cui è collocato il componente

Consultate le informazioni di base per:

* [Abilitazione del contrassegno per un componente](/help/communities/implementing-scoring.md#enableforcomponent)
* [Applicazione delle regole](/help/communities/implementing-scoring.md#applytopage)

### Regole di punteggio e regole secondarie incluse {#included-scoring-rules-and-sub-rules}

Nella versione beta sono incluse due regole di punteggio avanzate per la funzione [forum](/help/communities/functions.md#forum-function) (una per ciascun forum e per i componenti commenti della funzione forum):

1. `/libs/settings/community/scoring/rules/adv-comments-scoring`

   * `subRules[] =
/libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule`

1. `/libs/settings/community/scoring/rules/adv-forums-scoring`

   * `subRules[] =
/libs/settings/community/scoring/rules/sub-rules/adv-forums-rule
/libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner`

**Note:**

* I nodi `rules` e `sub-rules` sono entrambi di tipo `cq:Page`.

* `subRules` è un attributo di tipo Stringon [] sul  `jcr:content` nodo della regola.

* `sub-rules` può essere condiviso tra diverse regole di punteggio.

* `rules` devono trovarsi in una posizione di repository con l&#39;autorizzazione di lettura per tutti.

* I nomi delle regole devono essere univoci indipendentemente dalla posizione.

### Regole di Badging incluse {#included-badging-rules}

Nella release sono incluse due regole di contrassegno avanzate che corrispondono ai [forum avanzati e alle regole di punteggio dei commenti](#included-scoring-rules-and-sub-rules).

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**Note:**

* `rules` i nodi sono di tipo cq:Page.
* `rules` devono trovarsi in una posizione di repository con l&#39;autorizzazione di lettura per tutti.
* I nomi delle regole devono essere univoci indipendentemente dalla posizione.

