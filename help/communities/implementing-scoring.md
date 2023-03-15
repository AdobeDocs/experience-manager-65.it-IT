---
title: Punteggio e badge delle community
seo-title: Communities Scoring and Badges
description: Il punteggio e i badge di AEM Communities consentono di identificare e premiare i membri della community
seo-description: AEM Communities scoring and badges lets you identify and reward community members
uuid: d73683df-a413-4b3c-869c-67568bfdfcf6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ea033bb9-cb92-4c93-855f-8c902999378c
docset: aem65
tagskeywords: scoring, badging, badges, gamification
role: Admin
exl-id: 4aa857f7-d111-4548-8f03-f6d6c27acf51
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2868'
ht-degree: 2%

---

# Punteggio e badge delle community {#communities-scoring-and-badges}

## Panoramica {#overview}

La funzione di valutazione e badge di AEM Communities consente di identificare e premiare i membri della community.

I principali aspetti del punteggio e dei badge sono:

* [Assegnare i badge](#assign-and-revoke-badges) identificare il ruolo di un membro della comunità.

* [Attribuzione di base dei badge](#enable-scoring) ai membri per incoraggiarne la partecipazione (quantità di contenuto creato).

* [Assegnazione avanzata di badge](/help/communities/advanced.md) identificare i membri come esperti (qualità dei contenuti creati).

**Nota** l&#39;assegnazione dei badge è [non abilitato per impostazione predefinita](/help/communities/implementing-scoring.md#main-pars-text-237875536).

>[!CAUTION]
>
>La struttura di implementazione visibile in CRXDE Lite è soggetta a modifiche una volta che l’interfaccia utente diventa disponibile.

## Badge {#badges}

I badge vengono inseriti sotto il nome di un membro per indicare il suo ruolo o la sua posizione nella comunità. I badge possono essere visualizzati come immagine o come nome. Quando viene visualizzato come immagine, il nome viene incluso come testo alternativo per l’accessibilità.

Per impostazione predefinita, i badge si trovano nell’archivio all’indirizzo

* `/libs/settings/community/badging/images`

Se vengono memorizzati in una posizione diversa, tutti devono essere accessibili in lettura.

I distintivi sono differenziati in UGC per quanto riguarda il fatto che siano stati assegnati o sono stati guadagnati in base alle regole. Al momento, i badge assegnati vengono visualizzati come testo e i badge guadagnati vengono visualizzati come immagine.

### Interfaccia utente per la gestione dei badge {#badge-management-ui}

Le Comunità [Console badge](/help/communities/badges.md) offre la possibilità di aggiungere badge personalizzati che possono essere visualizzati per un membro guadagnato (assegnato) o quando assume un ruolo specifico nella comunità (assegnato).

### Badge assegnati {#assigned-badges}

I badge basati sul ruolo vengono assegnati da un amministratore ai membri della community in base al loro ruolo nella community.

I badge assegnati (e awared) sono memorizzati nel [SRP](/help/communities/srp.md) e non sono direttamente accessibili. Fino a quando non è disponibile un’interfaccia grafica, l’unico modo per assegnare i badge basati su ruoli consiste nel farlo con codice o cURL. Per istruzioni su cURL, consulta la sezione con titolo [Assegnare e revocare i badge](#assign-and-revoke-badges).

Nella versione sono inclusi tre badge basati sui ruoli:

* **moderatore**

   `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **gestore di gruppo**

   `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **membro privilegiato**

   `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

   ![badge assegnati](assets/assigned-badges.png)

### Badge aggiudicati {#awarded-badges}

I badge basati sui premi vengono assegnati dal servizio di punteggio ai membri della comunità in base alle regole applicate alla loro attività nella comunità.

Affinché i badge vengano visualizzati come ricompensa per l’attività, devono verificarsi due eventi:

* Il badge deve essere [abilitato](#enableforcomponent) per il componente feature.
* Le regole di valutazione e contrassegno devono essere [applicato](#applytopage) alla pagina (o predecessore) in cui il componente è posizionato.

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
>Le regole di valutazione possono essere configurate per assegnare punti negativi per i post contrassegnati come inappropriati e quindi influenzare il valore del punteggio. Tuttavia, una volta guadagnato un badge, questo non verrà rimosso automaticamente a causa di modifiche della regola di riduzione del punto di punteggio o della regola di punteggio.
>
>I badge assegnati possono essere revocati nello stesso modo dei badge assegnati. Consulta la sezione [Assegnare e revocare i badge](#assign-and-revoke-badges) sezione . I miglioramenti futuri includeranno un’interfaccia utente per gestire i badge dei membri.

### Badge personalizzati {#custom-badges}

I badge personalizzati possono essere installati utilizzando [Console badge](/help/communities/badges.md) e viene assegnato o specificato nelle regole di badging.

Quando vengono installati dalla console Badge , i badge personalizzati vengono replicati automaticamente nell’ambiente di pubblicazione.

## Abilita punteggio {#enable-scoring}

Il punteggio non è abilitato per impostazione predefinita. I passaggi fondamentali per l’impostazione e l’abilitazione del punteggio e del rilascio dei badge sono i seguenti:

* Identificare le regole per i punti di guadagno ([regole di punteggio](#scoring-rules)).
* Per i punti accumulati per regole di punteggio, assegna [badge](#badges) ([regole di badge](#badging-rules)).

* [Applicare le regole di valutazione e contrassegno a un sito community](#apply-rules-to-content).
* [Abilitazione del badge per le funzioni della community](#enable-badges-for-component).

Consulta la sezione [Test rapido](#quick-test) per abilitare il punteggio per un sito community utilizzando le regole di valutazione e contrassegno predefinite per forum e commenti.

### Applica regole al contenuto {#apply-rules-to-content}

Per abilitare il punteggio e i badge, aggiungi le proprietà `scoringRules` e `badgingRules` a qualsiasi nodo della struttura del contenuto del sito.

Se il sito è già pubblicato, dopo aver applicato tutte le regole e aver abilitato i componenti, ripubblica il sito.

Le regole che si applicano a un componente abilitato per i badging sono quelle per il nodo corrente o per il relativo predecessore.

Se il nodo è di tipo `cq:Page` (consigliato), quindi, utilizzando CRXDE|Lite, aggiungi le proprietà ai relativi `jcr:content` nodo.

| **Proprietà** | **Tipo** | **Descrizione** |
|---|---|---|
| badgingRules | Stringa | un elenco array di [regole di badge](#badging-rules) |
| scoringRules | Stringa | un elenco array di [regole di punteggio](#scoring-rules) |

>[!NOTE]
>
>Se una regola di punteggio sembra non avere alcun effetto sull’assegnazione dei badge, assicurati che la regola di punteggio non sia stata bloccata dalla proprietà scoringRules della regola di badging. Vedi la sezione con titolo [Regole di contrassegno](#badging-rules).

### Abilita badge per componente {#enable-badges-for-component}

Le regole di valutazione e di binding sono in vigore solo per le istanze di componenti che hanno abilitato il badging modificando la configurazione del componente in [modalità di authoring](/help/communities/author-communities.md).

Proprietà booleana, `allowBadges`, abilita/disabilita la visualizzazione dei badge per un’istanza di un componente. È configurabile nella [finestra di dialogo modifica componente](/help/communities/author-communities.md) per i componenti forum, QnA e commento tramite una casella di controllo etichettata **Badge di visualizzazione**.

#### Esempio : allowBadges per l’istanza del componente Forum {#example-allowbadges-for-forum-component-instance}

![enable-badges-component](assets/enable-badges-component.png)

>[!NOTE]
>
>Qualsiasi componente può essere sovrapposto per visualizzare i badge utilizzando il codice HBS presente in forum, QnA e commenti come esempio.

## Regole di valutazione {#scoring-rules}

Le regole di valutazione sono alla base del punteggio allo scopo di assegnare i badge.

Molto semplicemente, ogni regola di punteggio è un elenco di una o più regole secondarie. Le regole di valutazione vengono applicate al contenuto del sito della community per identificare le regole da applicare quando i badge sono abilitati.

Le regole di valutazione vengono ereditate ma non aggiunte. Esempio:

* Se la pagina2 contiene la regola di punteggio2 e la pagina1 della pagina precedente contiene la regola di punteggio1.
* Un’azione su un componente page2 richiamerà sia la regola1 che la regola2.
* Se entrambe le regole contengono sub-regole applicabili per la stessa `topic/verb`:

   * Solo la regola secondaria di rule2 influenzerà il punteggio.
   * I punteggi provenienti da entrambe le sottorubriche non vengono sommati.

Se è presente più di una regola di punteggio, i punteggi vengono mantenuti separatamente per ogni regola.

Le regole di punteggio sono nodi di tipo `cq:Page` con proprietà `jcr:content` nodo che specifica l’elenco di regole secondarie che lo definiscono.

I punteggi sono memorizzati in SRP.

>[!NOTE]
>
>Best practice: assegna un nome univoco a ciascuna regola di punteggio.
>
>I nomi delle regole di punteggio devono essere univoci a livello globale; non devono terminare con lo stesso nome.
>
>Un esempio di cosa *not* per eseguire:
>
>/libs/settings/community/scoring/rules/site1/forums-scoring
>/libs/settings/community/scoring/rules/site2/forums-scoring

### Regole di valutazione secondarie {#scoring-sub-rules}

Le regole del punteggio contengono le proprietà che descrivono i valori per la partecipazione alla community.

Ogni regola secondaria di punteggio identifica:

* Quali attività vengono monitorate?
* Quale funzione comunitaria specifica è coinvolta?
* Quanti punti sono attribuiti?

Per impostazione predefinita, i punti vengono assegnati al membro che esegue un&#39;azione, a meno che la regola secondaria non specifichi il proprietario del contenuto come destinatario dei punti ( `forOwner`).

Ogni regola secondaria può essere inclusa in una o più regole di punteggio.

Il nome della regola secondaria in genere segue il pattern di utilizzo di un *soggetto* , *oggetto* e *verbo*. Esempio:

* creazione-commento-membro
* voto riservato ai membri

Le sub-regole sono nodi di tipo `cq:Page` con proprietà `jcr:content`nodo che specifica [verbi e argomenti](#topics-and-verbs) .

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
     <li>deve esserci almeno una proprietà verbo</li>
     <li>il verbo deve essere inserito in tutte le lettere maiuscole</li>
     <li>possono essere presenti più proprietà verbo, ma non sono presenti duplicati</li>
     <li>il valore è il punteggio da applicare per questo evento</li>
     <li>il valore può essere positivo o negativo</li>
     <li>un elenco di verbi supportati nella versione è nella <a href="#topics-and-verbs">Argomenti e verbi</a> sezione</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>Stringa</td>
   <td>
    <ul>
     <li>facoltativo; limita la sottoregola ai componenti della community identificati da argomenti dell’evento</li>
     <li>se specificato : value è una stringa con più valori di argomenti dell'evento</li>
     <li>un elenco di argomenti nella versione è disponibile nella sezione <a href="#topics-and-verbs">Argomenti e verbi</a> sezione</li>
     <li>l'impostazione predefinita è applicata a tutti gli argomenti associati al verbo o ai verbi</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>Booleano</td>
   <td>
    <ul>
     <li>facoltativo; non pertinente quando un membro agisce in base a contenuti di sua proprietà</li>
     <li>se true, applica il punteggio al proprietario del contenuto su cui viene agito</li>
     <li>se false, applica il punteggio all'azione del membro</li>
     <li>il valore predefinito è false</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>scoringType</code></td>
   <td>Stringa</td>
   <td>
    <ul>
     <li>facoltativo; identifica il motore di punteggio</li>
     <li>se "basic", specifica il motore di punteggio in base alla quantità
      <ul>
       <li>incluso nella versione</li>
      </ul> </li>
     <li>se "advanced", specifica il motore di punteggio in base alla qualità e alla quantità
      <ul>
       <li>richiede un <a href="/help/communities/advanced.md">pacchetto aggiuntivo</a></li>
      </ul> </li>
     <li>Il valore predefinito è "basic"</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Regole di valutazione e sottoregole incluse {#included-scoring-rules-and-sub-rules}

Nella versione sono incluse due regole di punteggio per [Funzione Forum](/help/communities/functions.md#forum-function) (uno per ciascuno dei componenti Forum e Commenti della funzione Forum) :

1. /libs/settings/community/scoring/rules/comments-scoring

   * subRules[] = /libs/settings/community/scoring/rules/sub-rules/membro-comment-create /libs/settings/community/scoring/rules/sub-rules/membro-receive-vote /libs/settings/community/scoring/rules/sub-rules/membro-by-vote /libs/settings/community/scoring/rules/sub-rules/membr-is-moderated

1. /libs/settings/community/scoring/rules/forums-scoring

   * subRules[] = /libs/settings/community/scoring/rules/sub-rules/membro-forum-create /libs/settings/community/scoring/rules/sub-rules/membro-receive-vote /libs/settings/community/scoring/rules/sub-rules/membro-by-vote /libs/settings/community/scoring/rules/sub-rules/membr-is-moderated

**Note:**

* Entrambi `rules` e `sub-rules` i nodi sono di tipo cq:Page.

* `subRules` è un attributo di tipo String[] sulla regola `jcr:content` nodo.

* `sub-rules` possono essere condivisi tra diverse regole di punteggio.
* `rules` devono trovarsi in una posizione archivio con autorizzazione di lettura per tutti.

   * I nomi delle regole devono essere univoci indipendentemente dalla posizione.

### Attivazione di regole di valutazione personalizzate {#activating-custom-scoring-rules}

Eventuali modifiche o aggiunte apportate alle regole di punteggio o alle sotto-regole apportate nell’ambiente di authoring devono essere installate al momento della pubblicazione.

## Regole di contrassegno {#badging-rules}

Le regole di contrassegno collegano le regole di punteggio ai badge specificando:

* Regola di valutazione
* Punteggio necessario per ricevere un badge specifico

Le regole di accesso sono nodi di tipo `cq:Page` con proprietà `jcr:content` nodo che collega le regole di punteggio a punteggi e badge.

Le regole per il contrassegno consistono in un `thresholds` che è un elenco ordinato di punteggi mappati su badge. I punteggi devono essere ordinati in valore crescente. Esempio:

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * Un badge in bronzo è premiato per guadagnare 1 punto.

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * Un distintivo d&#39;argento viene assegnato quando sono stati accumulati 60 punti.

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * Un badge in oro è avvertito quando sono stati accumulati 80 punti.

Le regole di badging sono associate alle regole di punteggio, che determinano l’accumulo di punti. Vedi la sezione con titolo [Applica regole al contenuto](#apply-rules-to-content).

La `scoringRules` in una regola di badging è sufficiente limitare quali regole di punteggio possono essere associate a quella particolare regola di badging.

>[!NOTE]
>
>Procedure consigliate : crea immagini di badge univoche per ogni sito AEM.

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
   <td><em>(obbligatorio)</em> Una stringa con più valori del modulo 'number|path'
    <ul>
     <li>number = score</li>
     <li>| = tratto verticale (U+007C)</li>
     <li>percorso = percorso completo della risorsa immagine del badge</li>
    </ul> Le stringhe devono essere ordinate in modo che i numeri aumentino in valore e non deve apparire spazio vuoto tra il numero e il percorso.<br /> Esempio di voce :<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Stringa</td>
   <td><em>(facoltativo)</em> Identifica il motore di punteggio come "base" o "avanzato". Se desideri utilizzare il motore di valutazione avanzato, consulta <a href="/help/communities/advanced.md">Punteggio e badge avanzati</a>. Il valore predefinito è "basic".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Stringa</td>
   <td>(<em>facoltativo</em>) Una stringa con più valori per limitare la regola di badging agli eventi di punteggio identificati dalle regole di punteggio</td>
  </tr>
 </tbody>
</table>

### Regole di contrassegno incluse {#included-badging-rules}

Nella versione sono incluse due regole di badging corrispondenti alla variabile [Regole di valutazione per forum e commenti](#includedscoringrules).

* `/libs/settings/community/badging/rules/comments-badging`

* `/libs/settings/community/badging/rules/forums-badging`

**Note:**

* `rules` i nodi sono di tipo cq:Page.
* `rules` devono trovarsi in una posizione archivio con autorizzazione di lettura per tutti.

   * I nomi delle regole devono essere univoci indipendentemente dalla posizione.

### Attivazione di regole di badging personalizzate {#activating-custom-badging-rules}

Eventuali modifiche o aggiunte apportate alle regole di badging o alle immagini effettuate nell’ambiente di authoring devono essere installate al momento della pubblicazione.

## Assegnare e revocare i badge {#assign-and-revoke-badges}

I badge possono essere assegnati ai membri utilizzando [console membri](/help/communities/members.md#badges-tab) o utilizzando i comandi cURL a livello di programmazione.

I seguenti comandi cURL mostrano cosa è necessario per una richiesta HTTP per l’assegnazione e la revoca dei badge. Il formato di base è:

cURL -i -X POST -H *header* -u *segno* -F *funzionamento* -F *badge* *membro-profile-url*

*header* = intestazione personalizzata &quot;Accept:application/json&quot; da passare al server (richiesta)

*segno* = administrator-id:password per esempio : admin:admin

*funzionamento* = &quot;:operation=social:assignBadge&quot; OR &quot;:operation=social:deleteBadge&quot;

*badge* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* = la posizione del file immagine del badge nell&#39;archivio, ad esempio: /libs/settings/community/badging/images/moderator/jcr:content/moderator.png

*membro-profile-url* = l&#39;endpoint per il profilo del membro al momento della pubblicazione, ad esempio : https://&lt;server>:&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>La *membro-profile-url*:
>
>* Può fare riferimento a un’istanza di authoring se il [Servizio tunnel](/help/communities/users.md#tunnel-service) è abilitato.
>* Può essere un nome oscuro e casuale - vedi [Lista di controllo sicurezza](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) riguardante l’ID autorizzabile.


### Esempi: {#examples}

#### Assegnare un badge del moderatore {#assign-a-moderator-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

#### Revoca di un badge d&#39;argento assegnato {#revoke-an-assigned-silver-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:deleteBadge" -F "badgeContentPath=/libs/settings/community/badging/images/silver/jcr:content/silver.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

>[!NOTE]
>
>L’utilizzo di cURL per assegnare e revocare i badge funziona per qualsiasi immagine di badge, ma quando viene assegnata al posto di earned, vengono contrassegnati come badge assegnati e gestiti di conseguenza.

## Punteggio e badge per componenti personalizzati {#scoring-and-badges-for-custom-components}

Le regole di valutazione e di contrassegno possono essere create per i componenti personalizzati associando gli argomenti evento creati per il componente ai verbi.

## Argomenti e verbi {#topics-and-verbs}

Quando i membri interagiscono con le funzioni di Communities, vengono inviati eventi che possono attivare listener asincroni, come notifiche e punteggio.

L&#39;istanza SocialEvent di un componente registra gli eventi come `actions` che si verificano per `topic`. SocialEvent include un metodo per restituire un `verb` associato all’azione. C&#39;è un *n-1* rapporto tra `actions` e `verbs`.

Per i componenti comunità consegnati, le tabelle seguenti descrivono `verbs` definiti per ciascuna `topic` disponibile per l&#39;utilizzo in [assegnazione del punteggio alle regole secondarie](#scoring-sub-rules).

>[!NOTE]
>
>Una nuova proprietà booleana, `allowBadges`, abilita/disabilita la visualizzazione dei badge per un’istanza di un componente. Sarà configurabile in aggiornato [finestre di dialogo di modifica dei componenti](/help/communities/author-communities.md) tramite una casella di controllo etichettata **Badge di visualizzazione**.

**[Componente calendario](/help/communities/calendar.md)**
SocialEvent `topic`= com/adobe/cq/social/calendar

| **Verbo** | **Descrizione** |
|---|---|
| POST | un membro crea un evento calendario |
| AGGIUNGI | commenti dei membri su un evento calendario |
| AGGIORNA | modifica dell&#39;evento calendario o del commento del membro |
| ELIMINA | l&#39;evento o il commento del calendario del membro viene eliminato |

**[Componente Commenti](/help/communities/comments.md)**
SocialEvent `topic`= com/adobe/cq/social/comment

| **Verbo** | **Descrizione** |
|---|---|
| POST | crea un commento |
| AGGIUNGI | risposta del membro al commento |
| AGGIORNA | modifica del commento del membro |
| ELIMINA | il commento del membro viene eliminato |

**[Componente libreria file](/help/communities/file-library.md)**
SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **Verbo** | **Descrizione** |
|---|---|
| POST | crea una cartella |
| ATTACCO | il membro carica un file |
| AGGIORNA | un membro aggiorna una cartella o un file |
| ELIMINA | elimina una cartella o un file |

**[Componente Forum](/help/communities/forum.md)**
SocialEvent `topic`= com/adobe/cq/social/forum

| **Verbo** | **Descrizione** |
|---|---|
| POST | argomento del forum crea membri |
| AGGIUNGI | risposte dei membri all&#39;argomento del forum |
| AGGIORNA | argomento forum o risposta del membro viene modificato |
| ELIMINA | l&#39;argomento o la risposta del forum del membro è cancellata |

**[Componente Journal](/help/communities/blog-feature.md)**
SocialEvent `topic`= com/adobe/cq/social/journal

| **Verbo** | **Descrizione** |
|---|---|
| POST | crea un articolo di blog |
| AGGIUNGI | commenti di un membro su un articolo di blog |
| AGGIORNA | articolo o commento del blog del membro è modificato |
| ELIMINA | l&#39;articolo o il commento del blog del membro è stato cancellato |

**[Componente QnA](/help/communities/working-with-qna.md)**
SocialEvent `topic` = com/adobe/cq/social/qna

| **Verbo** | **Descrizione** |
|---|---|
| POST | crea una domanda QnA |
| AGGIUNGI | crea una risposta QnA |
| AGGIORNA | viene modificata la domanda o la risposta QnA del membro |
| SELEZIONA | risposta del membro selezionata |
| ANNULLA | la risposta del membro è deselezionata |
| ELIMINA | la domanda o la risposta QnA del membro viene eliminata |

**[Componente Recensioni](/help/communities/reviews.md)**
SocialEvent `topic`= com/adobe/cq/social/review

| **Verbo** | **Descrizione** |
|---|---|
| POST | crea revisione |
| AGGIORNA | modifica della revisione del membro |
| ELIMINA | la revisione del membro viene eliminata |

**[Componente di valutazione](/help/communities/rating.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/rating

| **Verbo** | **Descrizione** |
|---|---|
| AGGIUNGI VALUTAZIONE | il contenuto del membro è stato valutato |
| RIMUOVI VALUTAZIONE | il contenuto del membro è stato valutato in modo non corretto |

**[Componente di voto](/help/communities/voting.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/vote

| **Verbo** | **Descrizione** |
|---|---|
| AGGIUNGI VOTO | il contenuto del membro è stato votato |
| RIMUOVI VOTO | il contenuto del membro è stato respinto |

**Componenti abilitati per la moderazione**
SocialEvent `topic`= com/adobe/cq/social/moderation

| **Verbo** | **Descrizione** |
|---|---|
| RIFIUTA | contenuto del membro negato |
| FLAG-AS INAPPROPRIATO | il contenuto del membro è contrassegnato |
| NON APPROPRIATO | il contenuto del membro viene rimosso |
| ACCETTARE | il contenuto del membro è approvato dal moderatore |
| CHIUDI | il membro chiude il commento alle modifiche e alle risposte |
| APERTO | riapre il commento |

### Eventi dei componenti personalizzati {#custom-component-events}

Per un componente personalizzato, viene creata un&#39;istanza di SocialEvent per registrare gli eventi del componente come `actions` che si verificano per `topic`.

Per supportare il punteggio, SocialEvent deve sovrascrivere il metodo `getVerb()` in modo che `verb` viene restituito per ogni `action`. La `verb` restituita per un’azione può essere comunemente utilizzata (ad esempio `POST`) o uno specializzato per il componente (ad esempio `ADD RATING`). C&#39;è un *n-1* rapporto tra `actions` e `verbs`.

## Risoluzione dei problemi {#troubleshooting}

### I badge non compaiono {#badges-are-not-appearing}

Se al contenuto del sito web sono state applicate regole di valutazione e contrassegno, ma non sono stati avvertiti badge per alcuna attività, assicurati che i badge siano stati abilitati per l’istanza del componente.

Vedi [Abilita badge per componente](#enable-badges-for-component).

### La regola di punteggio non ha alcun effetto {#scoring-rule-has-no-effect}

Se sono state applicate regole di punteggio e contrassegno al contenuto del sito web e i badge vengono assegnati per alcune azioni, ma non per altre, verifica che la regola di badging non abbia limitato le regole di punteggio a cui si applica.

Consulta la sezione `scoringRules` proprietà di [Regole di contrassegno](#badging-rules).

### Typo sensibile a maiuscole e minuscole {#case-sensitive-typo}

La maggior parte delle proprietà e dei valori, in particolare i verbi, sono sensibili all&#39;uso di maiuscole e minuscole. I verbi devono essere tutti UPPERCASE quando utilizzati in una regola secondaria di punteggio.

Se la funzione non funziona come previsto, verifica che i dati siano stati immessi correttamente.

## Test rapido {#quick-test}

È possibile provare rapidamente il punteggio e il contrassegno utilizzando il [Esercitazione introduttiva](/help/communities/getting-started.md) (interattiva) sito :

* Accedi a CRXDE Lite durante l’authoring.
* Passa alla pagina di base:

   * /content/sites/it/jcr:content

* Aggiungi la proprietà badgingRules :

   * **Nome**: `badgingRules`
   * **Tipo**: `String`
   * Seleziona **Multi**
   * Seleziona **Aggiungi**
   * Inserisci `/libs/settings/community/badging/rules/forums-badging`
   * Seleziona **+**
   * Inserisci `/libs/settings/community/badging/rules/comments-badging`
   * Seleziona **OK**

* Aggiungi la proprietà scoringRules :

   * **Nome**: `scoringRules`
   * **Tipo**: `String`
   * Seleziona **Multi**
   * Seleziona **Aggiungi**
   * Inserisci `/libs/settings/community/scoring/rules/forums-scoring`
   * Seleziona **+**
   * Inserisci `/libs/settings/community/scoring/rules/comments-scoring`
   * Seleziona **OK**

* Seleziona **Salva tutto**.

![assegnazione del punteggio al test](assets/test-scoring-badging.png)

Successivamente, assicurati che i componenti forum e commenti consentano la visualizzazione dei badge:

* Di nuovo utilizzando CRXDE Lite.
* Passa al componente forum

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* Aggiungi la proprietà booleana allowBadges, se necessario, e accertati che sia true.

   * **Nome**: `allowBadges`
   * **Tipo**: `Boolean`
   * **Valore**: `true`

![test-forum-component](assets/test-forum-component.png)

Successivamente, [ripubblicare](/help/communities/sites-console.md#publishing-the-site) il sito della community.

Infine,

* Individua il componente nell’istanza di pubblicazione.
* Accedi come membro della community (ad esempio : weston.mccall@dodgit.com / password).
* Pubblica un nuovo argomento del forum.
* La pagina deve essere aggiornata per consentire la visualizzazione del badge.

   * Disconnessione e accesso come membro della community diverso (ad esempio: aaron.mcdonald@mailinator.com/password).

* Seleziona il Forum.

Questo dovrebbe guadagnare al membro della comunità un badge di bronzo visibile con il loro post sul forum a causa della prima soglia della regola di badging del forum che è un punteggio di 1.

![bronzo](assets/bronzebadge.png)

## Informazioni aggiuntive {#additional-information}

Per ulteriori informazioni, consulta [Nozioni di base sul punteggio e sui badge](/help/communities/configure-scoring.md) per sviluppatori.

Per informazioni sul motore di punteggio avanzato, consulta [Punteggio e badge avanzati](/help/communities/advanced.md).

La classifica configurabile [component](/help/communities/enabling-leaderboard.md) e [Funzione](/help/communities/functions.md#leaderboard-function) semplifica la visualizzazione dei membri e dei loro punteggi su un sito community.
