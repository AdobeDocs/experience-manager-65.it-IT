---
title: Punteggio e distintivi delle community
seo-title: Punteggio e distintivi delle community
description: ' punteggio e simboli AEM Communities consente di identificare e premiare i membri della community'
seo-description: ' punteggio e simboli AEM Communities consente di identificare e premiare i membri della community'
uuid: d73683df-a413-4b3c-869c-67568bfdfcf6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ea033bb9-cb92-4c93-855f-8c902999378c
docset: aem65
tagskeywords: scoring, badging, badges, gamification
translation-type: tm+mt
source-git-commit: 2daf00f17058de8b901848fcf1128a5ee9770368
workflow-type: tm+mt
source-wordcount: '2884'
ht-degree: 2%

---


# Punteggio e distintivi delle community {#communities-scoring-and-badges}

## Panoramica {#overview}

La funzione  punteggio e distintivi AEM Communities consente di identificare e premiare i membri della community.

I principali aspetti del punteggio e dei simboli sono:

* [Assegnare simboli](#assign-and-revoke-badges) per identificare il ruolo di un membro nella community.

* [Attribuzione di base di simboli](#enable-scoring) ai membri per incoraggiarne la partecipazione (quantità di contenuto creato).

* [Assegnazione avanzata di distintivi](/help/communities/advanced.md) per identificare i membri come esperti (qualità del contenuto creato).

**Tenere presente** che l&#39;assegnazione dei simboli [non è abilitata per impostazione predefinita](/help/communities/implementing-scoring.md#main-pars-text-237875536).

>[!CAUTION]
>
>La struttura di implementazione visibile in CRXDE Lite è soggetta a modifiche una volta che l’interfaccia utente diventa disponibile.

## Badge {#badges}

I distintivi sono posti sotto il nome di un membro per indicare il suo ruolo o la sua posizione nella comunità. I simboli possono essere visualizzati come immagine o come nome. Quando viene visualizzata come immagine, il nome viene incluso come testo alternativo per l&#39;accessibilità.

Per impostazione predefinita, i simboli si trovano nella directory archivio in

* `/libs/settings/community/badging/images`

Se memorizzati in un percorso diverso, tutti dovrebbero essere accessibili in lettura.

I distintivi sono differenziati in UGC se sono stati assegnati o sono stati guadagnati in base alle regole. Al momento, i simboli assegnati vengono visualizzati come testo e i simboli acquisiti vengono visualizzati come immagine.

### Interfaccia utente di gestione dei badge {#badge-management-ui}

La console [](/help/communities/badges.md) Badge community consente di aggiungere distintivi personalizzati che possono essere visualizzati per un membro al momento della ricezione (assegnazione) o quando questi assume un ruolo specifico nella comunità (assegnazione).

### Badge assegnati {#assigned-badges}

I simboli basati sul ruolo vengono assegnati da un amministratore ai membri della community in base al loro ruolo nella comunità.

I simboli assegnati (e assegnati) sono memorizzati nell&#39; [SRP](/help/communities/srp.md) selezionato e non sono direttamente accessibili. Fino a quando non sarà disponibile un&#39;interfaccia utente grafica, l&#39;unico modo per assegnare i simboli basati sui ruoli è farlo con codice o cURL. Per le istruzioni cURL, consultate la sezione intitolata [Assegna e revoca distintivi](#assign-and-revoke-badges).

Nella versione sono inclusi tre simboli basati sui ruoli:

* **moderatore**

   `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **manager del gruppo**

   `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **membro privilegiato**

   `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

   ![assegnatari](assets/assigned-badges.png)

### Badge aggiudicati {#awarded-badges}

Il servizio di assegnazione dei punteggi viene assegnato ai membri della comunità in base alle regole applicate alla loro attività nella comunità.

Affinché i simboli possano essere visualizzati come una ricompensa per l&#39;attività, devono accadere due cose:

* Il contrassegno deve essere [attivato](#enableforcomponent) per il componente feature.
* Le regole di punteggio e contrassegno devono essere [applicate](#applytopage) alla pagina (o antenato) in cui è collocato il componente.

Nel rilascio sono inclusi tre simboli basati sulla ricompensa:

* **oro**

   `/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

* **argento**

   `/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

* **bronzo**

   `/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   ![badge assegnati](assets/awarded-badges.png)

>[!NOTE]
>
>Le regole di punteggio possono essere configurate per assegnare punti negativi ai post contrassegnati come inappropriati e quindi per influenzare il valore del punteggio. Tuttavia, una volta ottenuto un contrassegno, questo non verrà rimosso automaticamente a causa di modifiche alla regola di riduzione del punto di punteggio o di valutazione.
>
>I simboli assegnati possono essere revocati allo stesso modo dei simboli assegnati. Vedere la sezione [Assegna e revoca distintivi](#assign-and-revoke-badges) . I miglioramenti futuri includeranno un&#39;interfaccia utente per gestire i simboli dei membri.

### Badge personalizzati {#custom-badges}

I simboli personalizzati possono essere installati utilizzando la console [](/help/communities/badges.md) Badge e assegnati o specificati nelle regole di contrassegno.

Se installati dalla console Badge, i simboli personalizzati vengono replicati automaticamente nell’ambiente di pubblicazione.

## Abilita punteggio {#enable-scoring}

Il punteggio non è abilitato per impostazione predefinita. I passaggi di base per l’impostazione e l’abilitazione del punteggio e dell’assegnazione dei simboli sono:

* Identificare le regole per i punti di guadagno (regole di[punteggio](#scoring-rules)).
* Per i punti accumulati per regole di punteggio, assegnate [simboli](#badges) (regole[di](#badging-rules)contrassegno).

* [Applica le regole di punteggio e contrassegno a un sito](#apply-rules-to-content)community.
* [Abilitare il contrassegno per le funzioni](#enable-badges-for-component)community.

Consultate la sezione [Test](#quick-test) rapido per abilitare il punteggio per un sito community utilizzando le regole di valutazione e contrassegno predefinite per forum e commenti.

### Applica regole al contenuto {#apply-rules-to-content}

Per abilitare il punteggio e i simboli, aggiungi le proprietà `scoringRules` e `badgingRules` a qualsiasi nodo della struttura del contenuto del sito.

Se il sito è già pubblicato, dopo aver applicato tutte le regole e attivato i componenti, ripubblicate il sito.

Le regole applicabili a un componente abilitato per il contrassegno sono quelle relative al nodo corrente o al suo predecessore.

Se il nodo è di tipo `cq:Page` (consigliato), aggiungere le proprietà al `jcr:content` nodo utilizzando CRXDE|Lite.

| **Proprietà** | **Tipo** | **Descrizione** |
|---|---|---|
| badgingRules | Stringa | un elenco matrice di regole di [contrassegno](#badging-rules) |
| scoringRules | Stringa | un elenco matrice di regole di [punteggio](#scoring-rules) |

>[!NOTE]
>
>Se una regola di punteggio non ha alcun effetto sull&#39;assegnazione dei simboli, assicurarsi che la regola di punteggio non sia stata bloccata dalla proprietà ScoringRules della regola di assegnazione contrassegno. Vedere la sezione intitolata [Regole](#badging-rules)di Badging.

### Abilita distintivi per componente {#enable-badges-for-component}

Le regole di punteggio e di binding sono valide solo per le istanze di componenti che hanno attivato il contrassegno modificando la configurazione del componente in modalità [](/help/communities/author-communities.md)Authoring.

Una proprietà booleana `allowBadges`abilita/disabilita la visualizzazione dei simboli per un’istanza di componente. È configurabile nella finestra di dialogo [di modifica del](/help/communities/author-communities.md) componente per i componenti forum, QnA e commento tramite una casella di controllo con l’etichetta **Display Badges**(Distinzionivisualizzazione).

#### Esempio: allowBadges per l’istanza del componente Forum {#example-allowbadges-for-forum-component-instance}

![enable-badges-component](assets/enable-badges-component.png)

>[!NOTE]
>
>Qualsiasi componente può essere sovrapposto per visualizzare i simboli utilizzando come esempio il codice HBS presente nei forum, QnA e nei commenti.

## Regole di punteggio {#scoring-rules}

Le regole di punteggio sono alla base del punteggio ai fini dell&#39;assegnazione dei distintivi.

Molto semplicemente, ogni regola di punteggio è un elenco di una o più regole secondarie. Le regole di punteggio vengono applicate al contenuto del sito della community per identificare le regole da applicare quando i simboli sono abilitati.

Le regole di punteggio vengono ereditate ma non aggiunte. Esempio:

* Se la pagina2 contiene la regola di punteggio2 e la pagina1 corrispondente contiene la regola di punteggio1.
* Un&#39;azione su un componente pagina2 richiamerà sia rule1 che rule2.
* Se entrambe le regole contengono sub-regole applicabili per lo stesso `topic/verb`:

   * Solo la regola secondaria di rule2 influirà sul punteggio.
   * I punteggi di entrambe le regole secondarie non vengono sommati.

Se è presente più di una regola di punteggio, i punteggi vengono mantenuti separatamente per ogni regola.

Le regole di punteggio sono nodi di tipo `cq:Page` con proprietà sul `jcr:content` nodo che specificano l&#39;elenco di regole secondarie che lo definiscono.

I punteggi sono memorizzati in SRP.

>[!NOTE]
>
>Best practice: assegnate un nome univoco a ciascuna regola di punteggio.
>
>I nomi delle regole di punteggio devono essere univoci a livello globale; non devono terminare con lo stesso nome.
>
>Un esempio di cosa *non* fare:
>
>/libs/settings/community/scoring/rules/site1/forums-scoring
>/libs/settings/community/scoring/rules/site2/forums-scoring

### Regole secondarie punteggio {#scoring-sub-rules}

Le regole secondarie del punteggio contengono le proprietà che descrivono i valori per la partecipazione alla comunità.

Ogni regola secondaria di punteggio identifica:

* Quali attività vengono monitorate?
* Quale funzione comunitaria specifica è coinvolta?
* Quanti punti vengono assegnati?

Per impostazione predefinita, i punti vengono assegnati al membro che agisce a meno che la regola secondaria non specifichi che il proprietario del contenuto riceve i punti ( `forOwner`).

Ciascuna regola secondaria può essere inclusa in una o più regole di punteggio.

Il nome della regola secondaria segue in genere il pattern di utilizzo di un *oggetto* , di un *oggetto* e di un *verbo*. Esempio:

* membro-commento-create
* membro-ricevente

Le regole secondarie sono nodi di tipo `cq:Page` con proprietà sul relativo `jcr:content`nodo che specificano i [verbi e gli argomenti](#topics-and-verbs) .

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
     <li>obbligatorio; il verbo corrisponde a un'azione di evento</li>
     <li>deve essere presente almeno una proprietà verbo</li>
     <li>il verbo deve essere inserito in tutto MAIUSCOLO</li>
     <li>possono essere presenti più proprietà verbo, ma non sono presenti duplicati</li>
     <li>il valore è il punteggio da applicare per l'evento</li>
     <li>il valore può essere positivo o negativo</li>
     <li>un elenco di verbi supportati nella release si trova nella sezione <a href="#topics-and-verbs">Argomenti e verbi</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>Stringa</td>
   <td>
    <ul>
     <li>optional; limita la regola secondaria ai componenti della community identificati dagli argomenti dell'evento</li>
     <li>se specificato : value è una stringa multivalore di argomenti evento</li>
     <li>un elenco di argomenti nella release si trova nella sezione <a href="#topics-and-verbs">Argomenti e verbi</a></li>
     <li>l'impostazione predefinita è applicabile a tutti gli argomenti associati al verbo o ai verbi</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>Booleano</td>
   <td>
    <ul>
     <li>optional; non pertinente quando un membro agisce in base al contenuto di cui è proprietario</li>
     <li>se true, applica la valutazione al proprietario del contenuto su cui viene eseguita la azione</li>
     <li>se false, applica il punteggio all'azione del membro</li>
     <li>il valore predefinito è false</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>scoringType</code></td>
   <td>Stringa</td>
   <td>
    <ul>
     <li>optional; identifica il motore di valutazione</li>
     <li>se "basic", specifica il motore di punteggio in base alla quantità
      <ul>
       <li>incluso nel rilascio</li>
      </ul> </li>
     <li>se "advanced", specifica il motore di punteggio in base alla qualità e alla quantità
      <ul>
       <li>richiede un pacchetto <a href="/help/communities/advanced.md">aggiuntivo</a></li>
      </ul> </li>
     <li>il valore predefinito è "basic"</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Regole di punteggio e regole secondarie incluse {#included-scoring-rules-and-sub-rules}

Nella release sono incluse due regole di punteggio per la funzione [](/help/communities/functions.md#forum-function) Forum (una per ciascuna delle componenti Forum e Commenti della funzione Forum):

1. /libs/settings/community/scoring/rules/comments-scoring

   * subRules[] =/libs/settings/community/scoring/rules/sub-rules/membro-comment-create/libs/settings/community/scoring/rules/sub-rules/membro-receive-vote/libs/settings/community/scoring/rules/sub-rules/Member-dare-voti/libs/settings/community/scoring/rules/sub-rules/membro-is moderated

1. /libs/settings/community/scoring/rules/forums-scoring

   * subRules[] =/libs/settings/community/scoring/rules/sub-rules/membro-forum-create/libs/settings/community/scoring/rules/sub-rules/membro-receive-Vote/libs/settings/community/scoring/rules/sub-rules/Member-dare-voti/libs/settings/community/scoring/rules/sub-rules/membro è moderato

**Note:**

* Entrambi `rules` e `sub-rules` i nodi sono di tipo cq:Page.

* `subRules` è un attributo di tipo String[] sul nodo della `jcr:content` regola.

* `sub-rules` può essere condiviso tra diverse regole di punteggio.
* `rules` devono trovarsi in una posizione di repository con l&#39;autorizzazione di lettura per tutti.

   * I nomi delle regole devono essere univoci indipendentemente dalla posizione.

### Attivazione delle regole di punteggio personalizzate {#activating-custom-scoring-rules}

Eventuali modifiche o aggiunte apportate alle regole di punteggio o alle regole secondarie nell’ambiente di authoring devono essere installate al momento della pubblicazione.

## Regole di Badking {#badging-rules}

Le regole di assegnazione del tag collegano le regole di punteggio ai simboli specificando:

* Regola punteggio
* Punteggio necessario per ottenere un contrassegno specifico

Le regole di Badging sono nodi di tipo `cq:Page` con proprietà sul `jcr:content` nodo che correlano le regole di punteggio a valutazioni e simboli.

Le regole per il contrassegno consistono in una `thresholds` proprietà obbligatoria che è un elenco ordinato di punteggi mappati a simboli. I punteggi devono essere ordinati in valore crescente. Esempio:

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * Un distintivo di bronzo è stato avvertito per guadagnare 1 punto.

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * Un distintivo d&#39;argento è assegnato quando 60 punti sono stati accumulati.

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * Un distintivo d&#39;oro è stato avvertito quando sono stati accumulati 80 punti.

Le regole di Badging sono associate a regole di punteggio, che determinano come si accumulano i punti. Consultate la sezione intitolata [Applica regole al contenuto](#apply-rules-to-content).

La `scoringRules` proprietà di una regola di contrassegno limita semplicemente le regole di punteggio che possono essere associate a quella particolare regola di contrassegno.

>[!NOTE]
>
>Best practice: create immagini di contrassegno univoche per ciascun sito AEM.

![configurazione badging-rule](assets/badging-rule-configuration.png)

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Tipo</th>
   <th>Valore Descrizione</th>
  </tr>
  <tr>
   <td>threshold</td>
   <td>Stringa</td>
   <td><em>(obbligatorio)</em> Una stringa con più valori nel formato 'numero|percorso'
    <ul>
     <li>number = score</li>
     <li>| = il carattere della linea verticale (U+007C)</li>
     <li>percorso = percorso completo della risorsa immagine del contrassegno</li>
    </ul> Le stringhe devono essere ordinate in modo che i numeri aumentino in valore e che non venga visualizzato spazio vuoto tra il numero e il percorso.<br /> Voce di esempio:<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Stringa</td>
   <td><em>(facoltativo)</em> Identifica il motore di valutazione come "base" o "avanzato". Se il motore di valutazione avanzato è desiderato, consulta <a href="/help/communities/advanced.md">Advanced Scoring and Badges</a>(Punteggio e distintivi avanzati). Il valore predefinito è "basic".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Stringa</td>
   <td>(<em>facoltativo</em>) Stringa con più valori per limitare la regola di contrassegno agli eventi di punteggio identificati dalle regole di punteggio</td>
  </tr>
 </tbody>
</table>

### Regole di Badging incluse {#included-badging-rules}

Nella release sono incluse due regole di badging corrispondenti alle regole di punteggio dei [forum e dei commenti](#includedscoringrules).

* `/libs/settings/community/badging/rules/comments-badging`

* `/libs/settings/community/badging/rules/forums-badging`

**Note:**

* `rules` i nodi sono di tipo cq:Page.
* `rules` devono trovarsi in una posizione di repository con l&#39;autorizzazione di lettura per tutti.

   * I nomi delle regole devono essere univoci indipendentemente dalla posizione.

### Attivazione delle regole di contrassegno personalizzate {#activating-custom-badging-rules}

Eventuali modifiche o aggiunte apportate alle regole di contrassegno o alle immagini nell’ambiente di authoring devono essere installate al momento della pubblicazione.

## Assegnazione e revoca di badge {#assign-and-revoke-badges}

I distintivi possono essere assegnati ai membri tramite la console [](/help/communities/members.md#badges-tab) Membri o a livello di programmazione tramite i comandi cURL.

I seguenti comandi cURL mostrano quanto è necessario per una richiesta HTTP di assegnazione e revoca dei simboli. Il formato di base è:

cURL -i -X POST -H *header* -u *signin* -F *operation* -F *badge* *membro-profile-url*

*header* = &quot;Accept:application/json&quot;intestazione personalizzata da trasmettere al server (richiesta)

*signin* = administrator-id:passwordad esempio : admin:admin

*operation* = &quot;:operation=social:assignBadge&quot; OPPURE &quot;:operation=social:deleteBadge&quot;

*badge* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* = la posizione del file di immagine del contrassegno nel repository, ad esempio: /libs/settings/community/badging/images/moderator/jcr:content/moderator.png

*Member-profile-url* = l&#39;endpoint per il profilo del membro alla pubblicazione, ad esempio: https://&lt;server>:&lt;porta>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>L’URL-profilo- *membro*:
>
>* Può fare riferimento a un&#39;istanza di autore se il servizio [](/help/communities/users.md#tunnel-service) Tunnel è abilitato.
>* Può trattarsi di un nome oscuro e casuale. Consulta Elenco [di controllo](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) protezione per gli ID autorizzabili.


### Esempi: {#examples}

#### Assegnazione di un contrassegno moderatore {#assign-a-moderator-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

#### Revoca di un distintivo d&#39;argento assegnato {#revoke-an-assigned-silver-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:deleteBadge" -F "badgeContentPath=/libs/settings/community/badging/images/silver/jcr:content/silver.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

>[!NOTE]
>
>L’utilizzo di cURL per assegnare e revocare i simboli funziona per qualsiasi immagine contrassegno, ma quando viene assegnata al posto di quella ottenuta, vengono contrassegnati come simboli assegnati e gestiti di conseguenza.

## Punteggio e Badge per componenti personalizzati {#scoring-and-badges-for-custom-components}

Le regole di punteggio e contrassegno possono essere create per i componenti personalizzati associando gli argomenti evento creati per il componente ai verbi.

## Argomenti e verbi {#topics-and-verbs}

Quando i membri interagiscono con le funzionalità delle community, vengono inviati eventi che possono attivare listener asincroni, come notifiche e punteggio.

L&#39;istanza SocialEvent di un componente registra gli eventi come `actions` si verificano per un `topic`. SocialEvent include un metodo per restituire un `verb` associato all&#39;azione. C&#39;è una relazione *n-1* tra `actions` e `verbs`.

Per i componenti comunità consegnati, le tabelle che seguono descrivono i `verbs` definiti per ogni sottomodulo `topic` disponibile per l&#39;utilizzo nelle [regole](#scoring-sub-rules)di punteggio.

>[!NOTE]
>
>Una nuova proprietà booleana `allowBadges`, abilita/disabilita la visualizzazione dei simboli per un’istanza di componente. Sarà configurabile nelle finestre di dialogo di modifica dei [componenti aggiornate](/help/communities/author-communities.md) tramite una casella di controllo con l’etichetta **Display Badges**.

**[Componente](/help/communities/calendar.md)** calendario SocialEvent `topic`= com/adobe/cq/social/calendario

| **Verbo** | **Descrizione** |
|---|---|
| POST | membro crea un evento del calendario |
| AGGIUNGI | commenti dei membri su un evento del calendario |
| AGGIORNA | evento del calendario del membro o commento modificato |
| ELIMINA | l&#39;evento o il commento del calendario del membro viene eliminato |

**[Componente](/help/communities/comments.md)** SocialEvent `topic`= com/adobe/cq/social/comment

| **Verbo** | **Descrizione** |
|---|---|
| POST | crea un commento |
| AGGIUNGI | risposta del membro al commento |
| AGGIORNA | commento del membro è stato modificato |
| ELIMINA | commento del membro è eliminato |

**[Componente](/help/communities/file-library.md)** Libreria file SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **Verbo** | **Descrizione** |
|---|---|
| POST | create una cartella |
| ATTACCO | il membro carica un file |
| AGGIORNA | il membro aggiorna una cartella o un file |
| ELIMINA | il membro elimina una cartella o un file |

**[Componente](/help/communities/forum.md)** forumSocialEvent `topic`= com/adobe/cq/social/forum

| **Verbo** | **Descrizione** |
|---|---|
| POST | membro crea argomento del forum |
| AGGIUNGI | risposte dei membri all&#39;argomento del forum |
| AGGIORNA | argomento forum o risposta del membro è modificato |
| ELIMINA | l&#39;argomento o la risposta del forum del membro viene eliminata |

**[Componente](/help/communities/blog-feature.md)** JournalSocialEvent `topic`= com/adobe/cq/social/journal

| **Verbo** | **Descrizione** |
|---|---|
| POST | un membro crea un articolo di blog |
| AGGIUNGI | commenti dei membri su un articolo di blog |
| AGGIORNA | articolo o commento del blog del membro è stato modificato |
| ELIMINA | l&#39;articolo o il commento del blog del membro viene eliminato |

**[QnA Component](/help/communities/working-with-qna.md)** SocialEvent `topic` = com/adobe/cq/social/qna

| **Verbo** | **Descrizione** |
|---|---|
| POST | un membro crea una domanda QnA |
| AGGIUNGI | un membro crea una risposta QnA |
| AGGIORNA | la domanda o la risposta QnA del membro viene modificata |
| SELECT | la risposta del membro è selezionata |
| ANNULLA | la risposta del membro è deselezionata |
| ELIMINA | la domanda o la risposta QnA del membro viene eliminata |

**[Recensioni Component](/help/communities/reviews.md)** SocialEvent `topic`= com/adobe/cq/social/review

| **Verbo** | **Descrizione** |
|---|---|
| POST | il membro crea una revisione |
| AGGIORNA | revisione membro |
| ELIMINA | la revisione del membro viene eliminata |

**[Classificazione componente](/help/communities/rating.md)** SocialEvent `topic`= com/adobe/cq/social/tally/rating

| **Verbo** | **Descrizione** |
|---|---|
| AGGIUNGI VALUTAZIONE | il contenuto del membro è stato valutato |
| RIMUOVI VALUTAZIONE | il contenuto del membro non è stato valutato |

**[Componente](/help/communities/voting.md)** di voto `topic`= com/adobe/cq/social/tally/Votazione

| **Verbo** | **Descrizione** |
|---|---|
| AGGIUNGI VOTO | il contenuto del membro è stato votato |
| RIMUOVI VOTO | il contenuto del membro è stato respinto |

**Componenti** SocialEvent abilitati per moderazione `topic`= com/adobe/cq/social/moderation

| **Verbo** | **Descrizione** |
|---|---|
| NEGA | contenuto del membro negato |
| FLAG-AS-INAPPROPRIATE | il contenuto del membro è contrassegnato |
| INAPPROPRIATO | contenuto del membro non contrassegnato |
| ACCETTARE | il contenuto del membro è approvato dal moderatore |
| CHIUDI | il membro chiude il commento alle modifiche e alle risposte |
| APRI | riapre commento membro |

### Eventi componente personalizzati {#custom-component-events}

Per un componente personalizzato, viene creata un&#39;istanza di SocialEvent per registrare gli eventi del componente come `actions` si verificano per un `topic`.

Per supportare il punteggio, SocialEvent deve sovrascrivere il metodo in `getVerb()` modo che venga restituito un punteggio `verb` adeguato per ogni `action`. Il `verb` valore restituito per un’azione può essere uno utilizzato comunemente (ad esempio `POST`) o uno specializzato per il componente (ad esempio `ADD RATING`). C&#39;è una relazione *n-1* tra `actions` e `verbs`.

## Risoluzione dei problemi {#troubleshooting}

### I simboli non vengono visualizzati {#badges-are-not-appearing}

Se al contenuto del sito Web sono state applicate regole di punteggio e contrassegno, ma i simboli non vengono avvertiti per alcuna attività, accertatevi che i simboli siano stati abilitati per l&#39;istanza del componente in questione.

Consultate [Abilitare i simboli per il componente](#enable-badges-for-component).

### La regola di punteggio non ha alcun effetto {#scoring-rule-has-no-effect}

Se al contenuto del sito Web sono state applicate regole di punteggio e contrassegno e i simboli vengono assegnati per alcune azioni, ma non per altre, verificate che la regola di contrassegno non abbia limitato le regole di punteggio a cui si applica.

Vedere la `scoringRules` proprietà delle regole di [Badging](#badging-rules).

### Composizione maiuscolo/minuscolo {#case-sensitive-typo}

La maggior parte delle proprietà e dei valori, in particolare i verbi, sono sensibili alle maiuscole/minuscole. I verbi devono essere tutti UPPERCASE se utilizzati in una regola secondaria di punteggio.

Se la funzione non funziona come previsto, verificare che i dati siano stati immessi correttamente.

## Test rapido {#quick-test}

È possibile provare rapidamente il punteggio e il contrassegno utilizzando il sito [Guida introduttiva all&#39;esercitazione](/help/communities/getting-started.md) :

* Accedere al CRXDE Lite sull&#39;autore.
* Passa alla pagina di base:

   * /content/sites/interazione/it/jcr:content

* Aggiungere la proprietà badgingRules:

   * **Nome**: `badgingRules`
   * **Tipo**: `String`
   * Seleziona **multipla**
   * Seleziona **Aggiungi**
   * Enter `/libs/settings/community/badging/rules/forums-badging`
   * Seleziona **+**
   * Enter `/libs/settings/community/badging/rules/comments-badging`
   * Selezionare **OK**

* Aggiungere la proprietà scoringRules:

   * **Nome**: `scoringRules`
   * **Tipo**: `String`
   * Seleziona **multipla**
   * Seleziona **Aggiungi**
   * Enter `/libs/settings/community/scoring/rules/forums-scoring`
   * Seleziona **+**
   * Enter `/libs/settings/community/scoring/rules/comments-scoring`
   * Selezionare **OK**

* Selezionate **Salva tutto**.

![test-punteggio](assets/test-scoring-badging.png)

Assicuratevi quindi che i componenti forum e commenti consentano la visualizzazione dei simboli:

* Utilizzando di nuovo CRXDE Lite.
* Passare al componente forum

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* Se necessario, aggiungere la proprietà booleana allowBadges e assicurarsi che sia vera.

   * **Nome**: `allowBadges`
   * **Tipo**: `Boolean`
   * **Valore**: `true`

![test-forum-component](assets/test-forum-component.png)

Quindi, [ripubblicate](/help/communities/sites-console.md#publishing-the-site) il sito della community.

Infine,

* Individuate il componente nell’istanza di pubblicazione.
* Accedi come membro della community (ad esempio: weston.mccall@dodgit.com / password).
* Pubblicare un nuovo argomento del forum.
* Per visualizzare il contrassegno, è necessario aggiornare la pagina.

   * Disconnessione e login come membro della community diverso (ad esempio: aaron.mcdonald@mailinator.com/password).

* Selezionate il forum.

Questo dovrebbe far sì che il membro della comunità un distintivo di bronzo visibile con il post del forum a causa della prima soglia della regola di tessitura del forum è un punteggio di 1.

![bronzebadge](assets/bronzebadge.png)

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Scoring and Badges Essentials](/help/communities/configure-scoring.md) per gli sviluppatori.

Per informazioni sul motore di valutazione avanzato, consulta [Advanced Scoring and Badges](/help/communities/advanced.md)(Punteggio e distintivi avanzati).

Il [componente](/help/communities/enabling-leaderboard.md) e la [funzione](/help/communities/functions.md#leaderboard-function) Leaderboard configurabili semplificano la visualizzazione dei membri e dei loro punteggi in un sito della community.
