---
title: Punteggio community e badge
description: Il punteggio e i badge di AEM Communities ti consentono di identificare e premiare i membri della community
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
tagskeywords: scoring, badging, badges, gamification
role: Admin
exl-id: 4aa857f7-d111-4548-8f03-f6d6c27acf51
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '2852'
ht-degree: 2%

---

# Punteggio community e badge {#communities-scoring-and-badges}

## Panoramica {#overview}

La funzione Punteggio e badge di AEM Communities consente di identificare e premiare i membri della community.

I principali aspetti del punteggio e dei distintivi sono:

* [Assegna badge](#assign-and-revoke-badges) identificare il ruolo di un membro nella comunità.

* [Assegnazione di base dei distintivi](#enable-scoring) ai membri di incoraggiare la loro partecipazione (quantità di contenuti creati).

* [Assegnazione avanzata di distintivi](/help/communities/advanced.md) identificare i membri come esperti (qualità dei contenuti creati).

**Nota** che il rilascio dei distintivi sia [non abilitato per impostazione predefinita](/help/communities/implementing-scoring.md#main-pars-text-237875536).

>[!CAUTION]
>
>La struttura di implementazione visibile in CRXDE Liti è soggetta a modifiche una volta che l’interfaccia utente diventa disponibile.

## Badge {#badges}

I badge sono posti sotto il nome di un membro per indicare il suo ruolo o la sua posizione nella comunità. I badge possono essere visualizzati come immagine o come nome. Quando viene visualizzato come immagine, il nome viene incluso come testo alternativo per l’accessibilità.

Per impostazione predefinita, i badge si trovano nell’archivio nei seguenti punti:

* `/libs/settings/community/badging/images`

Se vengono memorizzati in una posizione diversa, dovrebbero essere letti e accessibili a tutti.

I distintivi sono differenziati in UGC a seconda che siano stati assegnati o siano stati ottenuti in base alle regole. Al momento, i badge assegnati vengono visualizzati come testo e quelli guadagnati come immagine.

### Interfaccia utente per la gestione dei badge {#badge-management-ui}

Le comunità [Console badge](/help/communities/badges.md) consente di aggiungere distintivi personalizzati che possono essere visualizzati per un membro quando guadagnato (assegnato) o quando assume un ruolo specifico nella community (assegnato).

### Badge assegnati {#assigned-badges}

I badge basati sul ruolo vengono assegnati da un amministratore ai membri della community in base al loro ruolo all’interno della community.

I badge assegnati (e assegnati) sono memorizzati nel selezionato [SRP](/help/communities/srp.md) e non sono direttamente accessibili. Finché non sarà disponibile un’interfaccia utente grafica, l’unico modo per assegnare i badge basati sui ruoli consiste nell’utilizzare codice o cURL. Per le istruzioni cURL, consulta la sezione intitolata [Assegnare e revocare i badge](#assign-and-revoke-badges).

Nella versione sono inclusi tre badge basati sui ruoli:

* **moderatore**
  `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **manager gruppo**
  `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **membro privilegiato**
  `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

  ![assigned-badges](assets/assigned-badges.png)

### Distintivi assegnati {#awarded-badges}

I badge basati su premi vengono assegnati dal servizio di punteggio ai membri della community in base alle regole applicate alla loro attività nella community.

Affinché i distintivi vengano visualizzati come ricompensa per l’attività, è necessario che si verifichino due cose:

* La classificazione deve essere [abilitato](#enableforcomponent) per il componente funzione.
* Le regole di punteggio e contrassegno devono essere [applicato](#applytopage) alla pagina (o alla pagina precedente) in cui è posizionato il componente.

Nella versione sono inclusi tre badge basati su premi:

* **oro**
  `/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

* **argento**
  `/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

* **bronzo**
  `/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

  ![badge assegnati](assets/awarded-badges.png)

>[!NOTE]
>
>Le regole di punteggio possono essere configurate per assegnare punti negativi ai post contrassegnati come inappropriati e quindi influenzare il valore del punteggio. Tuttavia, una volta ottenuto un distintivo, non verrà rimosso automaticamente a causa della riduzione del punto di punteggio o di modifiche alla regola di punteggio.
>
>I badge assegnati possono essere revocati allo stesso modo dei badge assegnati. Consulta la [Assegnare e revocare i badge](#assign-and-revoke-badges) sezione. I miglioramenti futuri includeranno un’interfaccia utente per la gestione dei badge dei membri.

### Badge personalizzati {#custom-badges}

I badge personalizzati possono essere installati utilizzando [Console badge](/help/communities/badges.md) e sono assegnati o specificati nelle regole di badge.

Se installati dalla console Badge, i badge personalizzati vengono replicati automaticamente nell’ambiente di pubblicazione.

## Abilita punteggio {#enable-scoring}

Il punteggio non è abilitato per impostazione predefinita. I passaggi di base per impostare e abilitare il punteggio e l’assegnazione dei distintivi sono i seguenti:

* Identificare le regole per i punti di guadagno ([regole di punteggio](#scoring-rules)).
* Per i punti accumulati per regole di punteggio, assegna [badge](#badges) ([regole di assegnazione badge](#badging-rules)).

* [Applicare le regole di punteggio e badge a un sito community](#apply-rules-to-content).
* [Abilita contrassegno per le funzioni community](#enable-badges-for-component).

Consulta la [Test rapido](#quick-test) per abilitare il punteggio per un sito community utilizzando le regole predefinite di punteggio e contrassegno per forum e commenti.

### Applicare regole al contenuto {#apply-rules-to-content}

Per abilitare il punteggio e i badge, aggiungi le proprietà `scoringRules` e `badgingRules` a qualsiasi nodo nella struttura del contenuto del sito.

Se il sito è già pubblicato, dopo aver applicato tutte le regole e abilitato i componenti, ripubblica il sito.

Le regole applicabili a un componente abilitato per i badge sono quelle per il nodo corrente o il suo predecessore.

Se il nodo è di tipo `cq:Page` (consigliato), quindi utilizzando CRXDE|Lite, aggiungi le proprietà al relativo `jcr:content` nodo.

| **Proprietà** | **Tipo** | **Descrizione** |
|---|---|---|
| badgingRules | Stringa | un elenco di array di [regole di assegnazione badge](#badging-rules) |
| scoringRules | Stringa | un elenco di array di [regole di punteggio](#scoring-rules) |

>[!NOTE]
>
>Se una regola di punteggio sembra non avere alcun effetto sull’assegnazione dei badge, assicurati che non sia stata bloccata dalla proprietà scoringRules della regola di punteggio. Vedi la sezione intitolata [Regole di assegnazione dei badge](#badging-rules).

### Abilita badge per componente {#enable-badges-for-component}

Le regole di assegnazione e punteggio sono attive solo per le istanze dei componenti per i quali è stato abilitato il badge modificando la configurazione del componente in [modalità di authoring](/help/communities/author-communities.md).

Una proprietà booleana, `allowBadges`, attiva/disattiva la visualizzazione dei badge per un’istanza del componente. È configurabile in [finestra di dialogo per modifica componente](/help/communities/author-communities.md) per i componenti forum, controllo qualità e commento tramite una casella di controllo etichettata **Visualizza badge**.

#### Esempio: allowBadges per l’istanza del componente Forum {#example-allowbadges-for-forum-component-instance}

![enable-badges-component](assets/enable-badges-component.png)

>[!NOTE]
>
>Qualsiasi componente può essere sovrapposto per visualizzare i badge utilizzando come esempio il codice HBS presente in forum, domande e commenti.

## Regole punteggio {#scoring-rules}

Le regole di punteggio sono alla base del punteggio per l’assegnazione dei badge.

Ogni regola di punteggio è un elenco di una o più regole secondarie. Le regole di punteggio vengono applicate al contenuto del sito community per identificare le regole da applicare quando i badge sono abilitati.

Le regole di punteggio vengono ereditate ma non aggiunte. Ad esempio:

* Se la pagina2 contiene la regola di punteggio2 e la pagina padre1 contiene la regola di punteggio1.
* Un’azione su un componente page2 richiama sia la regola1 che la regola2.
* Se entrambe le regole contengono regole secondarie applicabili per lo stesso `topic/verb`:

   * Solo la sottoregola di rule2 influisce sul punteggio.
   * I punteggi di entrambe le sottoregole non vengono aggiunti.

In presenza di più regole di punteggio, i punteggi vengono mantenuti separatamente per ciascuna regola.

Le regole di punteggio sono nodi di tipo `cq:Page` con le proprietà sul relativo `jcr:content` che specificano l’elenco delle sottoregole che lo definiscono.

I punteggi vengono memorizzati in SRP.

>[!NOTE]
>
>Best practice: assegna un nome univoco a ogni regola di punteggio.
>
>I nomi delle regole di punteggio devono essere univoci a livello globale; non devono terminare con lo stesso nome.
>
>Un esempio di cosa *non* da fare:
>
>/libs/settings/community/scoring/rules/site1/forums-scoring
>/libs/settings/community/scoring/rules/site2/forums-scoring

### Sottoregole punteggio {#scoring-sub-rules}

Le sottoregole di punteggio contengono le proprietà che descrivono nel dettaglio i valori per la partecipazione alla community.

Ogni sottoregola di punteggio identifica:

* Quali attività vengono tracciate?
* Quale funzione specifica della community è coinvolta?
* Quanti punti vengono assegnati?

Per impostazione predefinita, i punti vengono assegnati al membro che esegue un&#39;azione, a meno che la regola secondaria non specifichi che il proprietario del contenuto riceve i punti ( `forOwner`).

Ogni regola secondaria può essere inclusa in una o più regole di punteggio.

Il nome della regola secondaria segue in genere il pattern dell’utilizzo di *oggetto*, *oggetto*, e *verbo*. Ad esempio:

* member-comment-create
* membro-ricevente-voto

I sottoruoli sono nodi di tipo `cq:Page` con le proprietà sul relativo `jcr:content`nodo che specifica [verbi e argomenti](#topics-and-verbs) .

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Tipo</th>
   <th> Valore Descrizione</th>
  </tr>
  <tr>
   <td><i><code>VERB</code></i></td>
   <td>Lungo</td>
   <td>
    <ul>
     <li>obbligatorio; il verbo corrisponde a un'azione evento</li>
     <li>deve essere presente almeno una proprietà verbo</li>
     <li>il verbo deve essere inserito in MAIUSCOLO</li>
     <li>possono esistere più proprietà verbo, ma non duplicati</li>
     <li>il valore è il punteggio da applicare per questo evento</li>
     <li>il valore può essere positivo o negativo</li>
     <li>un elenco di verbi supportati nella versione è nel <a href="#topics-and-verbs">Argomenti e verbi</a> sezione</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>Stringa</td>
   <td>
    <ul>
     <li>facoltativo; limita la regola secondaria ai componenti community identificati dagli argomenti dell’evento</li>
     <li>se specificato : valore è una stringa con più valori di argomenti evento</li>
     <li>un elenco di argomenti della versione è disponibile nella sezione <a href="#topics-and-verbs">Argomenti e verbi</a> sezione</li>
     <li>l'impostazione predefinita viene applicata a tutti gli argomenti associati ai verbi</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>Booleano</td>
   <td>
    <ul>
     <li>facoltativo; non pertinente quando il membro agisce sul contenuto di sua proprietà</li>
     <li>se true, applica il punteggio al proprietario del contenuto su cui viene eseguita l’azione</li>
     <li>se false, applica il punteggio al membro che intraprende un'azione</li>
     <li>il valore predefinito è false</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>scoringType</code></td>
   <td>Stringa</td>
   <td>
    <ul>
     <li>facoltativo; identifica il motore di punteggio</li>
     <li>se "base", specifica il motore di assegnazione del punteggio in base alla quantità
      <ul>
       <li>incluso nella versione</li>
      </ul> </li>
     <li>se "avanzato", specifica il motore di punteggio in base alla qualità e alla quantità
      <ul>
       <li>richiede un <a href="/help/communities/advanced.md">pacchetto aggiuntivo</a></li>
      </ul> </li>
     <li>il valore predefinito è "basic"</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Regole e sottoregole di punteggio incluse {#included-scoring-rules-and-sub-rules}

Nella versione sono incluse due regole di punteggio per [Funzione forum](/help/communities/functions.md#forum-function) (uno per ogni componente Forum e Commenti della funzione Forum ):

1. /libs/settings/community/scoring/rules/comments-scoring

   * subRules[] = /libs/settings/community/scoring/rules/sub-rules/member-comment-create /libs/settings/community/scoring/rules/sub-rules/member-receive-voting /libs/settings/community/scoring/rules/sub-rules/member-given-voting /libs/settings/community/scoring/rules/sub-rules/member-is-moderated

1. /libs/settings/community/scoring/rules/forums-scoring

   * subRules[] = /libs/settings/community/scoring/rules/sub-rules/member-forum-create /libs/settings/community/scoring/rules/sub-rules/member-receive-voting /libs/settings/community/scoring/rules/sub-rules/member-given-voting /libs/settings/community/scoring/rules/sub-rules/member-is-moderated

**Note:**

* Entrambi `rules` e `sub-rules` I nodi sono di tipo cq:Page.

* `subRules` è un attributo di tipo String[] su `jcr:content` nodo.

* `sub-rules` può essere condiviso tra varie regole di punteggio.
* `rules` deve trovarsi in una posizione dell’archivio con autorizzazione di lettura per tutti.

   * I nomi delle regole devono essere univoci indipendentemente dalla posizione.

### Attivazione di regole di punteggio personalizzate {#activating-custom-scoring-rules}

Eventuali modifiche o aggiunte apportate alle regole o alle sottoregole di punteggio nell’ambiente di authoring devono essere installate al momento della pubblicazione.

## Regole di assegnazione dei badge {#badging-rules}

Le regole di assegnazione dei badge collegano le regole di assegnazione dei punteggi ai badge specificando:

* Regola punteggio
* Punteggio necessario per ottenere un distintivo specifico

Le regole di assegnazione dei badge sono nodi di tipo `cq:Page` con le proprietà sul relativo `jcr:content` che correlano le regole di punteggio a punteggi e badge.

Le regole per il contrassegno sono costituite da un `thresholds` si tratta di un elenco ordinato di punteggi mappati su badge. I punteggi devono essere ordinati in modo crescente. Ad esempio:

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * Un distintivo di bronzo è assegnato per aver guadagnato un punto.

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * Un distintivo d&#39;argento viene assegnato quando sono stati accumulati 60 punti.

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * Un distintivo d&#39;oro viene assegnato quando sono stati accumulati 80 punti.

Le regole di assegnazione dei punteggi sono associate alle regole di assegnazione dei punteggi, che determinano l’accumulo dei punti. Vedi la sezione intitolata [Applicare regole al contenuto](#apply-rules-to-content).

Il `scoringRules` su una regola di badge limita semplicemente le regole di punteggio che possono essere abbinate a quella particolare regola di badge.

>[!NOTE]
>
>Best practice : crea immagini distintive univoche per ciascun sito AEM.

![badging-rule-configuration](assets/badging-rule-configuration.png)

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Tipo</th>
   <th>Valore Descrizione</th>
  </tr>
  <tr>
   <td>soglie</td>
   <td>Stringa</td>
   <td><em>(obbligatorio)</em> Una stringa con più valori del formato 'number|path'
    <ul>
     <li>number = score</li>
     <li>| = carattere della linea verticale (U+007C)</li>
     <li>path = percorso completo della risorsa immagine del badge</li>
    </ul> Le stringhe devono essere ordinate in modo che i numeri aumentino di valore e non venga visualizzato alcuno spazio tra il numero e il percorso.<br /> Voce di esempio:<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Stringa</td>
   <td><em>(facoltativo)</em> Identifica il motore di punteggio come "di base" o "avanzato". Per informazioni sul motore di punteggio avanzato, consulta <a href="/help/communities/advanced.md">Punteggio avanzato e badge</a>. Il valore predefinito è "basic".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Stringa</td>
   <td>(<em>facoltativo</em>a) Una stringa con più valori per limitare la regola di assegnazione dei punteggi agli eventi identificati dalle regole di assegnazione dei punteggi</td>
  </tr>
 </tbody>
</table>

### Regole di assegnazione dei badge incluse {#included-badging-rules}

Nella versione sono incluse due regole di badge che corrispondono alle [Regole per il punteggio di forum e commenti](#includedscoringrules).

* `/libs/settings/community/badging/rules/comments-badging`

* `/libs/settings/community/badging/rules/forums-badging`

**Note:**

* `rules` I nodi sono di tipo cq:Page.
* `rules` deve trovarsi in una posizione dell’archivio con autorizzazione di lettura per tutti.

   * I nomi delle regole devono essere univoci indipendentemente dalla posizione.

### Attivazione di regole di assegnazione dei badge personalizzate {#activating-custom-badging-rules}

Eventuali modifiche o aggiunte apportate alle regole di badge o alle immagini nell’ambiente di authoring devono essere installate al momento della pubblicazione.

## Assegnare e revocare i badge {#assign-and-revoke-badges}

I distintivi possono essere assegnati ai membri utilizzando [console dei membri](/help/communities/members.md#badges-tab) o a livello di programmazione utilizzando i comandi cURL.

I seguenti comandi cURL mostrano ciò che è necessario per una richiesta HTTP per l’assegnazione e la revoca dei badge. Il formato di base è:

cURL -i -X POST -H *intestazione* -u *accesso* -F *operazione* -F *badge* *member-profile-url*

*intestazione* = intestazione personalizzata &quot;Accept:application/json&quot; da passare al server (obbligatoria)

*accesso* = administrator-id:password, ad esempio : admin:admin

*operazione* = &quot;:operation=social:assignBadge&quot; OPPURE &quot;:operation=social:deleteBadge&quot;

*badge* = &quot;badgeContentPath=&quot;*badge-image-file*&quot;

*badge-image-file* = la posizione del file di immagine del badge nell’archivio, ad esempio : /libs/settings/community/badging/images/moderator/jcr:content/moderator.png

*member-profile-url* = l&#39;endpoint per il profilo del membro al momento della pubblicazione, ad esempio: https://&lt;server>:&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>Il *member-profile-url*:
>
>* Può fare riferimento a un’istanza Autore se [Servizio tunnel](/help/communities/users.md#tunnel-service) è abilitato.
>* Può essere un nome oscuro e casuale - vedi [Elenco di controllo della sicurezza](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) relativo all’ID autorizzabile.

### Esempi: {#examples}

#### Assegna un badge moderatore {#assign-a-moderator-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

#### Revoca di un distintivo silver assegnato {#revoke-an-assigned-silver-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:deleteBadge" -F "badgeContentPath=/libs/settings/community/badging/images/silver/jcr:content/silver.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

>[!NOTE]
>
>L’utilizzo di cURL per assegnare e revocare i badge funziona per qualsiasi immagine del badge, ma quando viene assegnata invece che ottenuta, viene contrassegnata come badge assegnati e gestita di conseguenza.

## Punteggio e badge per i componenti personalizzati {#scoring-and-badges-for-custom-components}

È possibile creare regole di punteggio e contrassegno per i componenti personalizzati associando gli argomenti dell’evento creati per il componente ai verbi.

## Argomenti e verbi {#topics-and-verbs}

Quando i membri interagiscono con le funzionalità delle community, vengono inviati eventi che possono attivare listener asincroni, come notifiche e punteggi.

L’istanza SocialEvent di un componente registra gli eventi come `actions` che si verificano per un `topic`. SocialEvent include un metodo per restituire un `verb` associato all’azione. È presente un *n-1* relazione tra `actions` e `verbs`.

Per i componenti community consegnati, le tabelle seguenti descrivono `verbs` definito per ogni `topic` disponibile per l’uso in [sottoregole di punteggio](#scoring-sub-rules).

>[!NOTE]
>
>Una nuova proprietà booleana, `allowBadges`, attiva/disattiva la visualizzazione dei badge per un’istanza del componente. È configurabile in aggiornato [finestre di dialogo per modifica del componente](/help/communities/author-communities.md) tramite una casella di controllo etichettata **Visualizza badge**.

**[Componente calendario](/help/communities/calendar.md)**
SocialEvent `topic`= com/adobe/cq/social/calendar

| **Verbo** | **Descrizione** |
|---|---|
| POST | il membro crea un evento calendario |
| AGGIUNGI | commenti dei membri su un evento calendario |
| AGGIORNA | evento calendario o commento del membro modificato |
| ELIMINA | l&#39;evento o il commento del calendario del membro viene eliminato |

**[Componente Commenti](/help/communities/comments.md)**
SocialEvent `topic`= com/adobe/cq/social/comment

| **Verbo** | **Descrizione** |
|---|---|
| POST | il membro crea un commento |
| AGGIUNGI | risposte dei membri al commento |
| AGGIORNA | commento del membro modificato |
| ELIMINA | commento del membro eliminato |

**[Componente Libreria file](/help/communities/file-library.md)**
SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **Verbo** | **Descrizione** |
|---|---|
| POST | il membro crea una cartella |
| ALLEGA | membro carica un file |
| AGGIORNA | il membro aggiorna una cartella o un file |
| ELIMINA | il membro elimina una cartella o un file |

**[Componente forum](/help/communities/forum.md)**
SocialEvent `topic`= com/adobe/cq/social/forum

| **Verbo** | **Descrizione** |
|---|---|
| POST | membro crea argomento forum |
| AGGIUNGI | risposte dei membri all&#39;argomento forum |
| AGGIORNA | l&#39;argomento del forum o la risposta del membro è stata modificata |
| ELIMINA | l&#39;argomento del forum o la risposta del membro è stata eliminata |

**[Componente diario](/help/communities/blog-feature.md)**
SocialEvent `topic`= com/adobe/cq/social/journal

| **Verbo** | **Descrizione** |
|---|---|
| POST | un membro crea un articolo di blog |
| AGGIUNGI | commenti dei membri su un articolo del blog |
| AGGIORNA | articolo del blog o commento di un membro è stato modificato |
| ELIMINA | l&#39;articolo o il commento del blog del membro è stato eliminato |

**[Componente D/R](/help/communities/working-with-qna.md)**
SocialEvent `topic` = com/adobe/cq/social/qna

| **Verbo** | **Descrizione** |
|---|---|
| POST | il membro crea una domanda di controllo qualità |
| AGGIUNGI | il membro crea una risposta QnA |
| AGGIORNA | domanda o risposta QnA del membro modificata |
| SELEZIONA | risposta del membro selezionata |
| DESELEZIONA | la risposta del membro è deselezionata |
| ELIMINA | la domanda o la risposta QnA del membro viene eliminata |

**[Componente Recensioni](/help/communities/reviews.md)**
SocialEvent `topic`= com/adobe/cq/social/review

| **Verbo** | **Descrizione** |
|---|---|
| POST | il membro crea la revisione |
| AGGIORNA | revisione del membro modificata |
| ELIMINA | revisione del membro eliminata |

**[Componente valutazione](/help/communities/rating.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/rating

| **Verbo** | **Descrizione** |
|---|---|
| AGGIUNGI VALUTAZIONE | il contenuto dell&#39;utente è stato rivalutato |
| RIMUOVI VALUTAZIONE | il contenuto dell&#39;utente non è stato valutato correttamente |

**[Componente voto](/help/communities/voting.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/voting

| **Verbo** | **Descrizione** |
|---|---|
| AGGIUNGI VOTAZIONE | il contenuto del membro è stato votato |
| RIMUOVI VOTAZIONE | il contenuto del membro non è stato votato |

**Componenti abilitati per moderazione**
SocialEvent `topic`= com/adobe/cq/social/moderation

| **Verbo** | **Descrizione** |
|---|---|
| RIFIUTA | contenuto dell&#39;utente negato |
| SEGNALA COME INAPPROPRIATO | il contenuto del membro è contrassegnato |
| ANNULLA SEGNALAZIONE COME INAPPROPRIATO | il contenuto del membro non è contrassegnato |
| ACCETTA | il contenuto del membro è approvato dal moderatore |
| CHIUDI | il membro chiude il commento alle modifiche e alle risposte |
| APRI | membro riapre commento |

### Eventi dei componenti personalizzati {#custom-component-events}

Per un componente personalizzato, viene creata un’istanza di SocialEvent per registrare gli eventi del componente come `actions` che si verificano per un `topic`.

Per supportare il punteggio, SocialEvent deve ignorare il metodo `getVerb()` in modo che un `verb` viene restituito per ogni `action`. Il `verb` restituito per un&#39;azione può essere uno dei valori comunemente utilizzati (ad esempio `POST`) o uno specifico per il componente (ad esempio `ADD RATING`). È presente un *n-1* relazione tra `actions` e `verbs`.

## Risoluzione dei problemi {#troubleshooting}

### I badge non vengono visualizzati {#badges-are-not-appearing}

Se sono state applicate regole di punteggio e badge al contenuto del sito web, ma i badge non vengono assegnati per alcuna attività, assicurati che i badge siano stati abilitati per l’istanza di quel componente.

Consulta [Abilita badge per componente](#enable-badges-for-component).

### La regola punteggio non ha alcun effetto {#scoring-rule-has-no-effect}

Se al contenuto del sito web sono state applicate regole di punteggio e badge e questi vengono assegnati per alcune azioni, ma non per altre, verifica che la regola di badge non abbia limitato le regole di punteggio a cui si applica.

Consulta la `scoringRules` proprietà di [Regole di assegnazione dei badge](#badging-rules).

### Tipo sensibile a maiuscole e minuscole {#case-sensitive-typo}

La maggior parte delle proprietà e dei valori, in particolare i verbi, fanno distinzione tra maiuscole e minuscole. I verbi devono essere tutti maiuscoli se utilizzati in una sottoregola di punteggio.

Se la funzione non funziona come previsto, assicurati che i dati siano stati immessi correttamente.

## Test rapido {#quick-test}

È possibile provare rapidamente a assegnare punteggi e contrassegni utilizzando [Tutorial introduttivo](/help/communities/getting-started.md) (coinvolgere) sito:

* Accedi a CRXDE Liti durante la creazione.
* Passa alla pagina base:

   * /content/sites/engagement/en/jcr:content

* Aggiungi la proprietà badgingRules:

   * **Nome**: `badgingRules`
   * **Tipo**: `String`
   * Seleziona **Più**
   * Seleziona **Aggiungi**
   * Inserisci `/libs/settings/community/badging/rules/forums-badging`
   * Seleziona **+**
   * Inserisci `/libs/settings/community/badging/rules/comments-badging`
   * Seleziona **OK**

* Aggiungere la proprietà scoringRules:

   * **Nome**: `scoringRules`
   * **Tipo**: `String`
   * Seleziona **Più**
   * Seleziona **Aggiungi**
   * Inserisci `/libs/settings/community/scoring/rules/forums-scoring`
   * Seleziona **+**
   * Inserisci `/libs/settings/community/scoring/rules/comments-scoring`
   * Seleziona **OK**

* Seleziona **Salva tutto**.

![test-scoring-badging](assets/test-scoring-badging.png)

Quindi, assicurati che i componenti forum e commenti consentano la visualizzazione dei badge:

* Di nuovo utilizzando CRXDE Liti.
* Passa al componente forum

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* Aggiungi la proprietà booleana allowBadges, se necessario, e assicurati che sia true.

   * **Nome**: `allowBadges`
   * **Tipo**: `Boolean`
   * **Valore**: `true`

![test-forum-component](assets/test-forum-component.png)

Avanti, [ripubblicare](/help/communities/sites-console.md#publishing-the-site) il sito della community.

Infine,

* Individua il componente nell’istanza di pubblicazione.
* Accedi come membro della community (ad esempio: weston.mccall@dodgit.com / password).
* Pubblica un nuovo argomento forum.
* Affinché il badge sia visibile, è necessario aggiornare la pagina.

   * Esci e accedi come membro diverso della community (ad esempio: aaron.mcdonald@mailinator.com/password).

* Selezionare il forum.

Questo dovrebbe far sì che il membro della community riceva un distintivo in bronzo visibile con il suo post sul forum, poiché la prima soglia della regola di assegnazione del badge ai forum è un punteggio di 1.

![bronzebadge](assets/bronzebadge.png)

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili sul sito [Nozioni di base su punteggio e distintivi](/help/communities/configure-scoring.md) pagina per sviluppatori.

Per informazioni sul motore di punteggio avanzato, consulta [Punteggio avanzato e badge](/help/communities/advanced.md).

La classifica configurabile [componente](/help/communities/enabling-leaderboard.md) e [funzione](/help/communities/functions.md#leaderboard-function) semplifica la visualizzazione dei membri e dei relativi punteggi in un sito community.
