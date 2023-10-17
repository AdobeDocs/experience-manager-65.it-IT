---
title: Punteggio avanzato e badge
description: Scopri come impostare il punteggio avanzato per consentire l’assegnazione di distintivi per identificare i membri come esperti.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: d3bb6664-6c01-4bcf-840c-072fc491fc99
source-git-commit: 0a4aca939c564720f63f055e9522e56942eaa128
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 1%

---

# Punteggio avanzato e badge{#advanced-scoring-and-badges}

## Panoramica {#overview}

Il punteggio avanzato consente di assegnare distintivi per identificare i membri come esperti. Il punteggio avanzato assegna punti in base alla quantità *e* qualità del contenuto creato da un membro, mentre il punteggio di base assegna punti in base alla quantità di contenuto creato.

Questa differenza è dovuta al motore di punteggio utilizzato per calcolare i punteggi. Il motore di punteggio di base applica una matematica semplice. Il motore di punteggio avanzato è un algoritmo adattivo che premia i membri attivi che contribuiscono a contenuti importanti e rilevanti, dedotti attraverso l’elaborazione del linguaggio naturale (NLP) di un argomento.

Oltre alla rilevanza dei contenuti, gli algoritmi di punteggio tengono conto delle attività dei membri, come le votazioni e la percentuale di risposte. Anche se il punteggio di base li include quantitativamente, il punteggio avanzato li utilizza in modo algoritmico.

Pertanto, il motore di punteggio avanzato richiede dati sufficienti per rendere l’analisi significativa. La soglia di successo per diventare un esperto viene costantemente rivalutata man mano che l’algoritmo si adatta continuamente al volume e alla qualità dei contenuti creati. Esiste anche un concetto di *decadimento* dei post più vecchi di un membro. Se un membro esperto smette di partecipare alla materia in cui ha ottenuto lo status di esperto, in un momento predeterminato (cfr. [configurazione del motore di punteggio](#configurable-scoring-engine)) potrebbero perdere il loro status di esperti.

L’impostazione del punteggio avanzato è praticamente identica al punteggio di base:

* Le regole di base e avanzate per punteggio e badge sono [applicato al contenuto](/help/communities/implementing-scoring.md#apply-rules-to-content) nello stesso modo.

   * Le regole di base e avanzate per il punteggio e i badge possono essere applicate allo stesso contenuto.

* [Abilitazione dei badge per i componenti](/help/communities/implementing-scoring.md#enable-badges-for-component) è generico.

Le differenze nell’impostazione delle regole di punteggio e badge sono:

* Motore di punteggio avanzato configurabile
* Regole di punteggio avanzate:

   * `scoringType` imposta su `advanced`
   * Richiede `stopwords`

* Regole di badge avanzate:

   * `badgingType` imposta su `advanced`
   * `badgingLevels` imposta su **numero di livelli di esperti da premiare**
   * Richiede `badgingPaths` array di badge invece delle soglie la mappatura degli array punta ai badge.

>[!NOTE]
>
>Per utilizzare le funzionalità avanzate di punteggio e badge, installa [Pacchetto di identificazione degli esperti](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq610%2Fsocial%2Ffeaturepack%2Fcq-social-expert-identification-pkg).

## Motore di punteggio configurabile {#configurable-scoring-engine}

Il motore di punteggio avanzato fornisce una configurazione OSGi con parametri che influiscono sull’algoritmo di punteggio avanzato.

![advanced-scoring-engine](assets/advanced-scoring-engine.png)

* **Pesi punteggio**

  Per un argomento, specifica il verbo a cui assegnare la priorità più elevata durante il calcolo del punteggio. È possibile immettere uno o più argomenti, ma è limitato a **un verbo per argomento**. Consulta [Argomenti e verbi](/help/communities/implementing-scoring.md#topics-and-verbs).
Immesso come `topic,verb` con escape virgola. Ad esempio:
  `/social/forum/hbs/social/forum\,ADD`
Il valore predefinito è impostato sul verbo ADD per i componenti QnA e forum.

* **Intervallo punteggio**

  L’intervallo per i punteggi avanzati è definito da questo valore (punteggio massimo) e da 0 (punteggio più basso possibile).

  Il valore predefinito è 100, quindi l’intervallo di punteggio è compreso tra 0 e 100.

* **Intervallo di tempo di decadimento entità**

  Questo parametro rappresenta il numero di ore dopo le quali tutti i punteggi di entità vengono decaduti. Questa opzione è necessaria per non includere più il contenuto precedente nei punteggi di un sito community.

  Il valore predefinito è 216000 ore (~24 anni).

* **Tasso di crescita del punteggio**
Questo specifica il punteggio tra 0 e l’intervallo di punteggio, oltre il quale la crescita rallenta per limitare il numero di esperti.

  Il valore predefinito è 50.

## Regole di punteggio avanzate {#advanced-scoring-rules}

Nel punteggio di base, è nota la quantità necessaria per ottenere un distintivo.

Nel caso del punteggio avanzato, la quantità necessaria viene costantemente adeguata in base alla quantità di dati di qualità all’interno del sistema. Il punteggio viene continuamente calcolato in modo simile a una curva a campana.

Se un membro ha ottenuto un distintivo di esperto su un argomento che non è più attivo, c’è la possibilità che perda il suo distintivo a causa di un decadimento nel tempo.

### scoringType {#scoringtype}

Una regola di punteggio è un set di regole secondarie di punteggio, ciascuna delle quali dichiara `scoringType`.

Per richiamare il motore di punteggio avanzato, `scoringType`deve essere impostato su `advanced`.

Consulta [Sottoregole punteggio](/help/communities/implementing-scoring.md#scoring-sub-rules).

![advanced-scoring-type](assets/advanced-scoring-type.png)

### Parole di arresto {#stopwords}

Il pacchetto di assegnazione punteggio avanzato installa una cartella di configurazione contenente un file di parole non significative:

* `/libs/settings/community/scoring/configuration/stopwords`

L’algoritmo di punteggio avanzato utilizza l’elenco di parole contenute nel file delle parole non significative per identificare le parole inglesi comuni che vengono ignorate durante l’elaborazione del contenuto.

Non ci si aspetta che questo file venga modificato.

Se manca il file delle parole d’arresto, il motore di punteggio avanzato restituisce un errore.

## Regole di assegnazione dei badge avanzate {#advanced-badging-rules}

Le proprietà della regola di badge avanzate sono diverse da [proprietà regola di assegnazione badge di base](/help/communities/implementing-scoring.md#badging-rules).

Invece di associare i punti a un’immagine del badge, è sufficiente identificare il numero di esperti ammessi e l’immagine del badge da assegnare.

![regole di badging avanzate](assets/advanced-badging-rules.png)

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
   <td><em>(Obbligatorio)</em> Una stringa con più valori di immagini di badge fino al numero di badgeLevels. I percorsi delle immagini del badge devono essere ordinati in modo che il primo venga assegnato al massimo esperto. Se il numero di badge è inferiore a quello indicato da badgingLevels, l’ultimo badge nell’array occuperà il resto dell’array. Esempio di voce:<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>Lungo</td>
   <td><em>(Facoltativo)</em> Specifica i livelli di esperienza da assegnare. Ad esempio, se deve essere <code>expert </code>e un <code>almost expert</code> (due badge), il valore deve essere impostato su 2. Il valore badgingLevel deve corrispondere al numero di immagini badge correlate all’esperto elencate per la proprietà badgingPath. Il valore predefinito è 1.</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Stringa</td>
   <td><em>(Obbligatorio)</em> Identifica il motore di punteggio come "di base" o "avanzato". Impostate questo parametro su "Advanced", altrimenti l'impostazione predefinita è "Basic".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Stringa[]</td>
   <td><em>(Facoltativo)</em> Una stringa con più valori per limitare la regola di assegnazione dei punteggi agli eventi di punteggio identificati da una o più regole di punteggio elencate.<br /> Esempio di voce:<br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> Il valore predefinito non prevede alcuna restrizione.</td>
  </tr>
 </tbody>
</table>

## Regole e badge inclusi {#included-rules-and-badge}

### Badge incluso {#included-badge}

In questa versione beta è incluso un distintivo per gli esperti basato su premi:

* `expert`

  `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![badge esperto](assets/included-badge.png)

Affinché il badge di esperto venga visualizzato come ricompensa per l’attività, assicurati:

* `Badges` sono abilitate per la funzione, ad esempio un forum o un componente QnA.

* Le regole avanzate di punteggio e badge vengono applicate alla pagina (o al predecessore) in cui viene posizionato il componente

Consulta le informazioni di base per:

* [Abilitazione del badge per un componente](/help/communities/implementing-scoring.md#enableforcomponent)
* [Applicazione delle regole](/help/communities/implementing-scoring.md#applytopage)

### Regole e sottoregole di punteggio incluse {#included-scoring-rules-and-sub-rules}

Nella versione beta sono incluse due regole di punteggio avanzate per [funzione forum](/help/communities/functions.md#forum-function) (uno ciascuno per i componenti forum e commenti della funzione forum):

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

* Entrambi `rules` e `sub-rules` i nodi sono di tipo `cq:Page`.
* `subRules` è un attributo di tipo String`[]` su `jcr:content` nodo.
* `sub-rules` può essere condiviso tra varie regole di punteggio.
* `rules` deve trovarsi in una posizione dell’archivio con autorizzazione di lettura per tutti.
* I nomi delle regole devono essere univoci indipendentemente dalla posizione.

### Regole di assegnazione dei badge incluse {#included-badging-rules}

Nella versione sono incluse due regole di badge avanzate che corrispondono alle [regole di punteggio per forum e commenti avanzati](#included-scoring-rules-and-sub-rules).

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**Note:**

* `rules` I nodi sono di tipo cq:Page.
* `rules` deve trovarsi in una posizione dell’archivio con autorizzazione di lettura per tutti.
* I nomi delle regole devono essere univoci indipendentemente dalla posizione.
