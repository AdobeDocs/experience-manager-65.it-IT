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
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2856'
ht-degree: 2%

---

# Punteggio community e badge {#communities-scoring-and-badges}

## Panoramica {#overview}

La funzione Punteggio e badge di AEM Communities consente di identificare e premiare i membri della community.

I principali aspetti del punteggio e dei distintivi sono:

* [Assegna badge](#assign-and-revoke-badges) per identificare il ruolo di un membro nella community.

* [Concessione di base di distintivi](#enable-scoring) ai membri per incoraggiarne la partecipazione (quantità di contenuti creati).

* [Assegnazione avanzata di distintivi](/help/communities/advanced.md) per identificare i membri come esperti (qualità del contenuto creato).

**Si noti** che l&#39;assegnazione dei distintivi è [non abilitata per impostazione predefinita](/help/communities/implementing-scoring.md#main-pars-text-237875536).

>[!CAUTION]
>
>La struttura di implementazione visibile in CRXDE Lite è soggetta a modifiche una volta che l’interfaccia utente diventa disponibile.

## Badge {#badges}

I badge sono posti sotto il nome di un membro per indicare il suo ruolo o la sua posizione nella comunità. I badge possono essere visualizzati come immagine o come nome. Quando viene visualizzato come immagine, il nome viene incluso come testo alternativo per l’accessibilità.

Per impostazione predefinita, i badge si trovano nell’archivio nei seguenti punti:

* `/libs/settings/community/badging/images`

Se vengono memorizzati in una posizione diversa, dovrebbero essere letti e accessibili a tutti.

I distintivi sono differenziati in UGC a seconda che siano stati assegnati o siano stati ottenuti in base alle regole. Al momento, i badge assegnati vengono visualizzati come testo e quelli guadagnati come immagine.

### Interfaccia utente per la gestione dei badge {#badge-management-ui}

La console [Badge](/help/communities/badges.md) per community consente di aggiungere distintivi personalizzati che possono essere visualizzati per un membro quando guadagnato (assegnato) o quando assume un ruolo specifico nella community (assegnato).

### Badge assegnati {#assigned-badges}

I badge basati sul ruolo vengono assegnati da un amministratore ai membri della community in base al loro ruolo all’interno della community.

I badge assegnati (e assegnati) sono archiviati nel [SRP](/help/communities/srp.md) selezionato e non sono direttamente accessibili. Finché non sarà disponibile un’interfaccia utente grafica, l’unico modo per assegnare i badge basati sui ruoli consiste nell’utilizzare codice o cURL. Per le istruzioni cURL, vedere la sezione [Assegnare e revocare i badge](#assign-and-revoke-badges).

Nella versione sono inclusi tre badge basati sui ruoli:

* **moderatore**
  `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **manager gruppo**
  `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **membro privilegiato**
  `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

  ![badge assegnati](assets/assigned-badges.png)

### Distintivi assegnati {#awarded-badges}

I badge basati su premi vengono assegnati dal servizio di punteggio ai membri della community in base alle regole applicate alla loro attività nella community.

Affinché i distintivi vengano visualizzati come ricompensa per l’attività, è necessario che si verifichino due cose:

* Il badge deve essere [abilitato](#enableforcomponent) per il componente funzionalità.
* Le regole per assegnazione punteggi e assegnazione badge devono essere [applicate](#applytopage) alla pagina (o al predecessore) in cui è posizionato il componente.

Nella versione sono inclusi tre badge basati su premi:

* **oro**
  `/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

* **argento**
  `/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

* **bronzo**
  `/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

  ![distintivi assegnati](assets/awarded-badges.png)

>[!NOTE]
>
>Le regole di punteggio possono essere configurate per assegnare punti negativi ai post contrassegnati come inappropriati e quindi influenzare il valore del punteggio. Tuttavia, una volta ottenuto un distintivo, non verrà rimosso automaticamente a causa della riduzione del punto di punteggio o di modifiche alla regola di punteggio.
>
>I badge assegnati possono essere revocati allo stesso modo dei badge assegnati. Consulta la sezione [Assegnare e revocare i badge](#assign-and-revoke-badges). I miglioramenti futuri includeranno un’interfaccia utente per la gestione dei badge dei membri.

### Badge personalizzati {#custom-badges}

I badge personalizzati possono essere installati utilizzando la [Console badge](/help/communities/badges.md) e assegnati o specificati nelle regole di badge.

Se installati dalla console Badge, i badge personalizzati vengono replicati automaticamente nell’ambiente di pubblicazione.

## Abilita punteggio {#enable-scoring}

Il punteggio non è abilitato per impostazione predefinita. I passaggi di base per impostare e abilitare il punteggio e l’assegnazione dei distintivi sono i seguenti:

* Identifica le regole per guadagnare punti ([regole punteggio](#scoring-rules)).
* Per i punti accumulati per le regole di punteggio, assegna [distintivi](#badges) ([regole di badge](#badging-rules)).

* [Applicare le regole di assegnazione dei punteggi e dei badge a un sito della community](#apply-rules-to-content).
* [Abilita il badge per le funzionalità della community](#enable-badges-for-component).

Consulta la sezione [Test rapido](#quick-test) per abilitare il punteggio per un sito community utilizzando le regole predefinite di punteggio e contrassegno per forum e commenti.

### Applicare regole al contenuto {#apply-rules-to-content}

Per abilitare il punteggio e i badge, aggiungere le proprietà `scoringRules` e `badgingRules` a qualsiasi nodo nella struttura del contenuto del sito.

Se il sito è già pubblicato, dopo aver applicato tutte le regole e abilitato i componenti, ripubblica il sito.

Le regole applicabili a un componente abilitato per i badge sono quelle per il nodo corrente o il suo predecessore.

Se il nodo è di tipo `cq:Page` (consigliato) e quindi si utilizza CRXDE|Lite, aggiungere le proprietà al nodo `jcr:content`.

| **Proprietà** | **Tipo** | **Descrizione** |
|---|---|---|
| badgingRules | Stringa | un elenco di array di [regole di badging](#badging-rules) |
| scoringRules | Stringa | un elenco di array di [regole di punteggio](#scoring-rules) |

>[!NOTE]
>
>Se una regola di punteggio sembra non avere alcun effetto sull’assegnazione dei badge, assicurati che non sia stata bloccata dalla proprietà scoringRules della regola di punteggio. Vedere la sezione con titolo [Regole di assegnazione dei badge](#badging-rules).

### Abilita badge per componente {#enable-badges-for-component}

Le regole di assegnazione e punteggio sono attive solo per le istanze dei componenti per i quali è stato abilitato il contrassegno modificando la configurazione del componente in [modalità di creazione](/help/communities/author-communities.md).

Una proprietà booleana, `allowBadges`, abilita/disabilita la visualizzazione dei badge per un&#39;istanza del componente. È configurabile nella [finestra di dialogo per modifica dei componenti](/help/communities/author-communities.md) per i componenti forum, QnA e commento tramite una casella di controllo etichettata **Distintivi di visualizzazione**.

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

Le regole di punteggio sono nodi di tipo `cq:Page` con proprietà nel nodo `jcr:content` che specificano l&#39;elenco di regole secondarie che lo definiscono.

I punteggi vengono memorizzati in SRP.

>[!NOTE]
>
>Best practice: assegna un nome univoco a ogni regola di punteggio.
>
>I nomi delle regole di punteggio devono essere univoci a livello globale; non devono terminare con lo stesso nome.
>
>Esempio di cosa *non* fare:
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

Il nome della regola secondaria segue in genere il modello di utilizzo di un *oggetto*, *oggetto* e *verbo*. Ad esempio:

* member-comment-create
* membro-ricevente-voto

I substrati sono nodi di tipo `cq:Page` con proprietà nel nodo `jcr:content` che specificano i [verbi e argomenti](#topics-and-verbs).

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Tipo</th>
   <th> Descrizione valore</th>
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
     <li>un elenco di verbi supportati nella versione è disponibile nella sezione <a href="#topics-and-verbs">Argomenti e verbi</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>Stringa</td>
   <td>
    <ul>
     <li>facoltativo; limita la regola secondaria ai componenti community identificati dagli argomenti dell’evento</li>
     <li>se specificato : valore è una stringa con più valori di argomenti evento</li>
     <li>un elenco di argomenti della versione è disponibile nella sezione <a href="#topics-and-verbs">Argomenti e verbi</a></li>
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

Nella versione sono incluse due regole di punteggio per la [funzione forum](/help/communities/functions.md#forum-function) (una per ogni componente Forum e Commenti della funzione forum):

1. /libs/settings/community/scoring/rules/comments-scoring

   * subRules[] =
/libs/settings/community/scoring/rules/sub-rules/member-comment-create
/libs/settings/community/scoring/rules/sub-rules/member-receive-voting
/libs/settings/community/scoring/rules/sub-rules/member-given-voting
/libs/settings/community/scoring/rules/sub-rules/member-is-moderated

1. /libs/settings/community/scoring/rules/forums-scoring

   * subRules[] =
/libs/settings/community/scoring/rules/sub-rules/member-forum-create
/libs/settings/community/scoring/rules/sub-rules/member-receive-voting
/libs/settings/community/scoring/rules/sub-rules/member-given-voting
/libs/settings/community/scoring/rules/sub-rules/member-is-moderated

**Note:**

* Entrambi i nodi `rules` e `sub-rules` sono di tipo cq:Page.

* `subRules` è un attributo di tipo String[] nel nodo `jcr:content` della regola.

* `sub-rules` può essere condiviso tra varie regole di punteggio.
* `rules` deve trovarsi in un percorso archivio con autorizzazione di lettura per tutti.

   * I nomi delle regole devono essere univoci indipendentemente dalla posizione.

### Attivazione di regole di punteggio personalizzate {#activating-custom-scoring-rules}

Eventuali modifiche o aggiunte apportate alle regole o alle sottoregole di punteggio nell’ambiente di authoring devono essere installate al momento della pubblicazione.

## Regole di assegnazione dei badge {#badging-rules}

Le regole di assegnazione dei badge collegano le regole di assegnazione dei punteggi ai badge specificando:

* Regola punteggio
* Punteggio necessario per ottenere un distintivo specifico

Le regole di assegnazione dei punteggi sono nodi di tipo `cq:Page` con proprietà nel nodo `jcr:content` che correlano le regole di assegnazione dei punteggi a punteggi e badge.

Le regole per i badge sono costituite da una proprietà `thresholds` obbligatoria che è un elenco ordinato di punteggi mappati ai badge. I punteggi devono essere ordinati in modo crescente. Ad esempio:

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * Un distintivo di bronzo è assegnato per aver guadagnato un punto.

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * Un distintivo d&#39;argento viene assegnato quando sono stati accumulati 60 punti.

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * Un distintivo d&#39;oro viene assegnato quando sono stati accumulati 80 punti.

Le regole di assegnazione dei punteggi sono associate alle regole di assegnazione dei punteggi, che determinano l’accumulo dei punti. Vedere la sezione con titolo [Applica regole al contenuto](#apply-rules-to-content).

La proprietà `scoringRules` di una regola di badge limita semplicemente le regole di punteggio che possono essere associate a quella particolare regola di badge.

>[!NOTE]
>
>Best practice : crea immagini distintive univoche per ciascun sito AEM.

![badging-rule-configuration](assets/badging-rule-configuration.png)

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Tipo</th>
   <th>Descrizione valore</th>
  </tr>
  <tr>
   <td>soglie</td>
   <td>Stringa</td>
   <td><em>(obbligatorio)</em> Stringa con più valori nel formato 'number|path'
    <ul>
     <li>number = score</li>
     <li>| = carattere della linea verticale (U+007C)</li>
     <li>path = percorso completo della risorsa immagine del badge</li>
    </ul> Le stringhe devono essere ordinate in modo che i numeri aumentino di valore e non venga visualizzato alcuno spazio tra il numero e il percorso.<br /> Voce di esempio:<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Stringa</td>
   <td><em>(facoltativo)</em> identifica il motore di punteggio come "di base" o "avanzato". Per informazioni sul motore di punteggio avanzato, vedere <a href="/help/communities/advanced.md">Punteggio avanzato e distintivi</a>. Il valore predefinito è "basic".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Stringa</td>
   <td>(<em>facoltativo</em>) Stringa con più valori per limitare la regola di assegnazione dei badge agli eventi di punteggio identificati dalle regole di assegnazione dei punteggi</td>
  </tr>
 </tbody>
</table>

### Regole di assegnazione dei badge incluse {#included-badging-rules}

Nella versione sono incluse due regole di assegnazione dei punteggi che corrispondono alle [regole di assegnazione dei punteggi per forum e commenti](#includedscoringrules).

* `/libs/settings/community/badging/rules/comments-badging`

* `/libs/settings/community/badging/rules/forums-badging`

**Note:**

* `rules` nodi sono di tipo cq:Page.
* `rules` deve trovarsi in un percorso archivio con autorizzazione di lettura per tutti.

   * I nomi delle regole devono essere univoci indipendentemente dalla posizione.

### Attivazione di regole di assegnazione dei badge personalizzate {#activating-custom-badging-rules}

Eventuali modifiche o aggiunte apportate alle regole di badge o alle immagini nell’ambiente di authoring devono essere installate al momento della pubblicazione.

## Assegnare e revocare i badge {#assign-and-revoke-badges}

I badge possono essere assegnati ai membri utilizzando la [console membri](/help/communities/members.md#badges-tab) o a livello di programmazione utilizzando i comandi cURL.

I seguenti comandi cURL mostrano ciò che è necessario per una richiesta HTTP per l’assegnazione e la revoca dei badge. Il formato di base è:

cURL -i -X POST -H *intestazione* -u *firma* -F *operazione* -F *distintivo* *membro-profilo-url*

*intestazione* = &quot;Accept:application/json&quot;
intestazione personalizzata da passare al server (obbligatoria)

*accesso* = administrator-id:password
ad esempio, admin:admin

*operation* = &quot;:operation=social:assignBadge&quot; OPPURE &quot;:operation=social:deleteBadge&quot;

*badge* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* = percorso del file di immagine del badge nell&#39;archivio
ad esempio, /libs/settings/community/badging/images/moderator/jcr:content/moderator.png

*member-profile-url* = endpoint per il profilo del membro al momento della pubblicazione
ad esempio, https://&lt;server>:&lt;porta>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>*member-profile-url*:
>
>* È possibile fare riferimento a un&#39;istanza di authoring se il servizio [Tunnel](/help/communities/users.md#tunnel-service) è abilitato.
>* Può essere un nome casuale oscuro. Vedere [Elenco di controllo protezione](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) relativo all&#39;ID autorizzabile.

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

L&#39;istanza SocialEvent di un componente registra gli eventi come `actions` che si verificano per un `topic`. SocialEvent include un metodo per restituire un `verb` associato all&#39;azione. Esiste una relazione *n-1* tra `actions` e `verbs`.

Per i componenti community consegnati, le tabelle seguenti descrivono i `verbs` definiti per ogni `topic` disponibile nelle [sottoregole di punteggio](#scoring-sub-rules).

>[!NOTE]
>
>Una nuova proprietà booleana, `allowBadges`, abilita/disabilita la visualizzazione dei badge per un&#39;istanza del componente. È configurabile nelle [finestre di dialogo di modifica dei componenti](/help/communities/author-communities.md) aggiornate tramite una casella di controllo con etichetta **Distintivi visualizzati**.

**[Componente Calendario](/help/communities/calendar.md)**
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

**[Componente Libreria File](/help/communities/file-library.md)**
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

**[Componente QnA](/help/communities/working-with-qna.md)**
SocialEvent `topic` = com/adobe/cq/social/qna

| **Verbo** | **Descrizione** |
|---|---|
| POST | il membro crea una domanda di controllo qualità |
| AGGIUNGI | il membro crea una risposta QnA |
| AGGIORNA | domanda o risposta QnA del membro modificata |
| SELEZIONA | risposta del membro selezionata |
| DESELEZIONA | la risposta del membro è deselezionata |
| ELIMINA | la domanda o la risposta QnA del membro viene eliminata |

**[Componente recensioni](/help/communities/reviews.md)**
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

**[Componente Votazione](/help/communities/voting.md)**
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

Per un componente personalizzato, viene creata un&#39;istanza di SocialEvent per registrare gli eventi del componente come `actions` che si verificano per `topic`.

Per supportare il punteggio, SocialEvent deve eseguire l&#39;override del metodo `getVerb()` in modo che venga restituito un `verb` appropriato per ogni `action`. Il `verb` restituito per un&#39;azione può essere uno usato comunemente (ad esempio `POST`) o uno specializzato per il componente (ad esempio `ADD RATING`). Esiste una relazione *n-1* tra `actions` e `verbs`.

## Risoluzione dei problemi {#troubleshooting}

### I badge non vengono visualizzati {#badges-are-not-appearing}

Se sono state applicate regole di punteggio e badge al contenuto del sito web, ma i badge non vengono assegnati per alcuna attività, assicurati che i badge siano stati abilitati per l’istanza di quel componente.

Vedere [Abilitare i badge per il componente](#enable-badges-for-component).

### La regola punteggio non ha alcun effetto {#scoring-rule-has-no-effect}

Se al contenuto del sito web sono state applicate regole di punteggio e badge e questi vengono assegnati per alcune azioni, ma non per altre, verifica che la regola di badge non abbia limitato le regole di punteggio a cui si applica.

Vedere la proprietà `scoringRules` di [Regole di assegnazione dei badge](#badging-rules).

### Tipo sensibile a maiuscole e minuscole {#case-sensitive-typo}

La maggior parte delle proprietà e dei valori, in particolare i verbi, fanno distinzione tra maiuscole e minuscole. I verbi devono essere tutti maiuscoli se utilizzati in una sottoregola di punteggio.

Se la funzione non funziona come previsto, assicurati che i dati siano stati immessi correttamente.

## Test rapido {#quick-test}

È possibile provare rapidamente a assegnare punteggi e contrassegni utilizzando il sito [Esercitazione introduttiva](/help/communities/getting-started.md) (coinvolgimento):

* Accedi a CRXDE Lite durante la creazione.
* Passa alla pagina base:

   * /content/sites/engagement/en/jcr:content

* Aggiungi la proprietà badgingRules:

   * **Nome**: `badgingRules`
   * **Tipo**: `String`
   * Seleziona **Più**
   * Seleziona **Aggiungi**
   * Immetti `/libs/settings/community/badging/rules/forums-badging`
   * Seleziona **+**
   * Immetti `/libs/settings/community/badging/rules/comments-badging`
   * Seleziona **OK**

* Aggiungere la proprietà scoringRules:

   * **Nome**: `scoringRules`
   * **Tipo**: `String`
   * Seleziona **Più**
   * Seleziona **Aggiungi**
   * Immetti `/libs/settings/community/scoring/rules/forums-scoring`
   * Seleziona **+**
   * Immetti `/libs/settings/community/scoring/rules/comments-scoring`
   * Seleziona **OK**

* Seleziona **Salva tutto**.

![test-scoring-badging](assets/test-scoring-badging.png)

Quindi, assicurati che i componenti forum e commenti consentano la visualizzazione dei badge:

* Di nuovo utilizzando CRXDE Lite.
* Passa al componente forum

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* Aggiungi la proprietà booleana allowBadges, se necessario, e assicurati che sia true.

   * **Nome**: `allowBadges`
   * **Tipo**: `Boolean`
   * **Valore**: `true`

![test-forum-component](assets/test-forum-component.png)

Successivamente, [ripubblica](/help/communities/sites-console.md#publishing-the-site) il sito della community.

Infine,

* Individua il componente nell’istanza di pubblicazione.
* Accedi come membro della community (ad esempio, weston.mccall@dodgit.com / password).
* Post un nuovo argomento forum.
* Affinché il badge sia visibile, è necessario aggiornare la pagina.

   * Esci e accedi come membro diverso della community (ad esempio: aaron.mcdonald@mailinator.com/password).

* Selezionare il forum.

Questo dovrebbe far sì che il membro della community riceva un distintivo in bronzo visibile con il suo post sul forum, poiché la prima soglia della regola di assegnazione del badge ai forum è un punteggio di 1.

![bronzebadge](assets/bronzebadge.png)

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Nozioni fondamentali su punteggio e distintivi](/help/communities/configure-scoring.md) per gli sviluppatori.

Per informazioni sul motore di punteggio avanzato, vedere [Punteggio avanzato e distintivi](/help/communities/advanced.md).

La classifica configurabile [componente](/help/communities/enabling-leaderboard.md) e [funzione](/help/communities/functions.md#leaderboard-function) semplifica la visualizzazione dei membri e dei relativi punteggi in un sito community.
