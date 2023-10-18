---
title: Moderazione dei contenuti della community
description: Scopri come moderare i contenuti generati dagli utenti in modo da poter riconoscere i contributi positivi e limitare quelli negativi, come lo spam e il linguaggio abusivo.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 22276580-e6bc-41c5-9ac3-e8f291f676b7
source-git-commit: 00b6f2f03470aca7f87717818d0dfcd17ac16bed
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 2%

---

# Moderazione dei contenuti della community {#moderating-community-content}

## Panoramica {#overview}

Il contenuto della community, noto anche come contenuto generato dall&#39;utente (UGC, User-Generated Content), viene creato quando un membro (visitatore del sito connesso) pubblica contenuti da un sito pubblicato della community tramite l&#39;interazione con uno dei seguenti componenti della community:

* [Blog](/help/communities/blog-feature.md): i membri pubblicano un articolo o un commento sul blog.
* [Calendario](/help/communities/calendar.md): i membri pubblicano un evento o un commento del calendario.
* [Commenti](/help/communities/comments.md): i membri pubblicano un commento o rispondono a un commento.

* [Forum](/help/communities/forum.md): i membri pubblicano un nuovo argomento o rispondono a un argomento.
* [Ideazione](/help/communities/ideation-feature.md): i membri pubblicano un&#39;idea o un commento.
* [D/R](/help/communities/working-with-qna.md): i membri creano una domanda o rispondono a una domanda.
* [Recensioni](/help/communities/reviews.md): i membri pubblicano un commento durante la valutazione di un elemento.

La moderazione dell’UGC è utile per riconoscere i contributi positivi e limitare quelli negativi (come spam e linguaggio abusivo). L’UGC può essere moderato da diversi ambienti:

* [Archiviazione di contenuti community](working-with-srp.md)

* [Console di moderazione in blocco](moderation.md)

  La console di moderazione è accessibile agli amministratori e [moderatori community](/help/communities/users.md) nell’ambiente pubblico e dagli amministratori nell’ambiente di authoring. Ciò è possibile quando il contenuto della community viene memorizzato in una [archivio comune](/help/communities/working-with-srp.md).

* [Moderazione nel contesto](in-context.md)

  La moderazione nell&#39;ambiente di pubblicazione può essere eseguita da amministratori e moderatori della community direttamente sulla pagina in cui è stato pubblicato il contenuto.

## Azioni di moderazione {#moderation-actions}

Le azioni che possono essere eseguite sui contenuti pubblicati (UGC, Post Content) variano a seconda dell’identità dell’utente e dell’ambiente. La tabella seguente utilizza la terminologia seguente per descrivere i vari ruoli in base all’identità dell’utente:

* `Admin`

  Un utente che è membro di [amministratori di community](users.md) gruppo.

* `Moderator`

  Membro di un [moderatori community](users.md#publishenvironmentusersandgroups) gruppo (ha [autorizzazioni moderatore](in-context.md#moderatorpermissions)).

* `Creator`

  Utente che ha pubblicato il contenuto.

* `Member`

  Utente connesso senza autorizzazioni speciali.

* `Visitor`

  Utente anonimo.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Amministratore</strong></td>
   <td><strong>Moderatore</strong></td>
   <td><strong>Creatore</strong></td>
   <td><strong>Membro</strong></td>
   <td><strong>Visitatore</strong></td>
   <td><strong>Evento<br /> Attivato</strong></td>
   <td><strong>Premoderato</strong></td>
  </tr>
  <tr>
   <td><strong>Modifica/<br /> Elimina</strong></td>
   <td>X</td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Taglia</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Rifiuta</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Chiudi/<br /> Riapri</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X<br /> </td>
  </tr>
  <tr>
   <td><strong>Contrassegno/<br /> Annulla contrassegno</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Consenti</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X</td>
  </tr>
 </tbody>
</table>

### Modifica/Elimina {#edit-delete}

Dopo aver creato un post, è possibile modificarlo o eliminarlo dal creatore, da un amministratore o dal moderatore della community.

Quando l’UGC viene eliminato, viene rimosso dall’archivio e potrebbe non essere ripristinato.

### Taglia {#cut}

Un amministratore o un moderatore della community può spostare uno o più argomenti di forum o domande di controllo qualità da una posizione a un’altra. Ciò include il passaggio da un sito di community a un altro, a condizione che lo stesso membro disponga dei privilegi di moderazione su entrambi i siti.

Selezionando l’azione Taglia, il contenuto viene copiato negli Appunti. È possibile copiare e spostare più post come gruppo nella nuova posizione.

![cutugc](assets/cutugc.png)

![putbackugc](assets/putbackugc.png)

Nell&#39;altra posizione, quando il contenuto è presente negli Appunti, accanto a Nuovo post è visibile un pulsante Incolla con un numero che identifica il numero di post che verranno incollati. Il pulsante Incolla include un’opzione per cancellare gli Appunti invece di incollarli.

![pasteugc](assets/pasteugc.png)

![pasteugc1](assets/pasteugc1.png)

### Rifiuta {#deny}

Un moderatore potrebbe impedire a UGC di rimanere visibile sul sito pubblicato. Per gli amministratori e i moderatori della community, il post è ancora disponibile e viene annotato come spam.

### Chiudi/Riapri {#close-reopen}

L&#39;azione Chiudi viene eseguita sull&#39;intero thread della conversazione (un argomento forum o il commento iniziale) e include tutti i post o le risposte successivi.

Quando è chiusa, non solo non è possibile fornire ulteriori risposte, ma non è consentita alcuna azione di moderazione.

Per eseguire qualsiasi operazione, è necessario riaprire l&#39;argomento o il commento.

L&#39;azione Chiudi/Riapri può essere eseguita da amministratori o moderatori della community.

### Contrassegna/Annulla contrassegno {#flag-unflag}

Il contrassegno è un mezzo per qualsiasi membro che ha effettuato l’accesso, ad eccezione dell’autore del contenuto, per indicare che si è verificato un problema con il contenuto di un post. Una volta contrassegnato, viene visualizzata un’icona di rimozione del contrassegno che consente allo stesso membro di rimuovere il contrassegno dal contenuto.

La moderazione nel contesto può essere configurata in modo da consentire ai membri di selezionare un motivo quando contrassegnano un post. L’elenco dei motivi del flag selezionabili è configurabile e specifica se è possibile inserire un motivo personalizzato. Il motivo del flag viene salvato con l&#39;UGC, ma non attiva alcuna azione particolare. Solo il numero di flag attiva una notifica. Il contenuto contrassegnato viene annotato come tale, in modo che i moderatori possano agire di conseguenza.

Il sistema tiene traccia di tutti i flag, di chi li ha contrassegnati e del motivo del flag e invia un evento quando viene raggiunta la soglia. Se l&#39;UGC è Consentito da un moderatore della community, questi flag vengono archiviati. Dopo aver consentito e archiviato, se sono presenti segnalazioni successive, queste verranno archiviate come se non fossero presenti segnalazioni precedenti.

### Consenti {#allow}

L’azione Consenti è un’opzione per contenuti generati dagli utenti che è stata Segnalata, Negata o non è stata approvata in un sistema con pre-moderazione. L’azione Consenti cancella qualsiasi stato contrassegnato o Negato/Spam presente e archivia tutti i dati contrassegnati.

## Concetti comuni relativi alla moderazione {#common-moderation-concepts}

### Premoderazione {#premoderation}

Quando l&#39;UGC è premoderato, il post non viene visualizzato sul sito pubblicato fino a quando non viene approvato da un&#39;azione di moderazione. Durante la creazione di un’ [sito community](/help/communities/sites-console.md), selezionando la casella [Il contenuto è premoderato](sites-console.md#moderation) abilita la premoderazione per l&#39;intero sito. Quando i componenti vengono inseriti in una pagina, i componenti che supportano la moderazione possono essere configurati per la premoderazione utilizzando un’impostazione nella finestra di dialogo per modifica:

* [Commenti](comments.md) e [recensioni](reviews.md)
in **[!UICONTROL Moderazione utenti]** > **[!UICONTROL Pre-moderazione]**.

* [Forum](/help/communities/forum.md), [ideazione](/help/communities/ideation-feature.md), [D/R](/help/communities/working-with-qna.md), e [calendario](/help/communities/calendar.md)
in **[!UICONTROL Impostazioni]** > **[!UICONTROL Moderato]**.

### Rilevamento posta indesiderata {#spam-detection}

Il rilevamento spam è una funzionalità di moderazione automatica che filtra parti indesiderate di contenuti generati dall’utente contrassegnandole come spam. Una volta attivato, identifica se un contenuto generato dall’utente è spam o meno in base a una raccolta preconfigurata di parole spam. Le parole spam predefinite vengono fornite in

`/libs/settings/community/sites/moderation/spamdetector-conf/profiles/spam_words.txt`.

Tuttavia, per personalizzare o estendere le parole spam predefinite, crea un set di parole nella directory /apps seguendo la struttura delle parole spam predefinite con [sovrapposizione](/help/communities/overlay-comments.md).

Un post generato dall’utente (per tutti i tipi di contenuto, ad esempio blog, forum e commenti) contenente spam word è contrassegnato con il testo &quot;Questo post è stato classificato come spam&quot; sopra il post.

Il moderatore può visualizzare un post di questo tipo e contrassegnarlo per consentire o negare la visualizzazione sul sito. Le azioni di moderazione su questi post possono essere eseguite nel contesto o tramite l&#39;interfaccia utente per la moderazione in blocco.

![spamdetection](assets/spamdetection.png)

Per abilitare il motore di rilevamento di posta indesiderata, effettua le seguenti operazioni:

1. Apri [Console web](https://localhost:4502/system/console/configMgr), da `/system/console/configMgr`.

1. Individua **Moderazione automatica AEM Communities** e modificarla.
1. Aggiungi il **[!UICONTROL SpamProcess]** voce.

![spamprocess](assets/spamprocess.png)

>[!NOTE]
>
>Il rilevamento spam è implementato solo per le lingue inglesi.

### Sentimento {#sentiment}

La valutazione viene calcolata in base al numero di parole chiave positive e negative ([parole d&#39;ordine](#configuringwatchwords)) presente in un post (UGC).

L’analisi del sentiment utilizza un set di regole preconfigurate e calcola il sentiment dell’UGC. Le regole predefinite si trovano in `/libs/cq/workflow/components/workflow/social/sentiments/rules`.

Il valore generato dalle regole va da 1 (tutte le parole negative, nessuna parola positiva) a 10 (tutte le parole positive, nessuna parola negativa). Il valore 5 è un sentimento neutro ed è l&#39;impostazione predefinita.

Le regole definite nel componente /libs sono:

* Regola 1: imposta il valore su 1 se non ci sono parole positive e almeno una parola negativa.
* Regola 2: imposta il valore su 10 se non ci sono parole negative e almeno una parola positiva.
* Regola 3: imposta il valore su 3 se il numero di parole negative è maggiore di quello positivo.
* Regola 4: imposta il valore su 8 se il numero di parole positive è superiore a quello di parole negative.

Per sovrascrivere o aggiungere regole, creare un set di regole nella directory /apps seguendo la struttura delle regole predefinite. Modifica la configurazione della valutazione in modo da identificare la posizione delle regole.

Una volta analizzato, il sentiment viene memorizzato con l&#39;UGC.

Dalla sezione [console di moderazione in blocco](/help/communities/moderation.md), è possibile filtrare e visualizzare i contenuti generati dagli utenti (UGC) in base al fatto che l’opinione sia negativa, neutra o positiva.

#### Parole di controllo {#watchwords}

AEM Communities fornisce una *watchword analyzer* come fase del processo di valutazione [sentiment](#sentiment). Il contributo al valore di valutazione fornito dalle parole d&#39;ordine è dovuto a un confronto tra le parole d&#39;ordine negative e positive utilizzate nel contenuto pubblicato e le parole non consentite.

#### Configura sentiment e parole d&#39;ordine {#configure-sentiment-and-watchwords}

L’elenco delle parole d’ordine positive e negative può essere personalizzato così come le regole di valutazione.

L’elenco predefinito di parole d’ordine può essere inserito come proprietà di un nodo nell’archivio, in modo simile all’elenco predefinito o escludendo l’elenco predefinito tramite la configurazione del servizio OSGi `sentimentprocess.name` con l&#39;elenco delle parole.

Il **sentimentprocess.name** può anche essere modificato per fare riferimento alla posizione di un set personalizzato di regole di valutazione.

Per configurare il sentiment e le parole d’ordine:

* Accedi all’istanza di authoring come amministratore.
* Apri [Console web](https://localhost:4502/system/console/configMgr).
* Individua `sentimentprocess.name`.
* Seleziona la configurazione in modo da poterla aprire in modalità di modifica.

![sentimentprocess](assets/sentimentprocess.png)

* **Parole di controllo positive**

  Elenco separato da virgole di parole che contribuiscono a un&#39;opinione positiva che ignora le impostazioni predefinite. L&#39;elenco predefinito è vuoto.

* **Parole di controllo negative**

  Elenco separato da virgole di parole che contribuiscono a un&#39;opinione negativa che ignora le impostazioni predefinite. L&#39;elenco predefinito è vuoto.

* **Percorso esplicito al nodo parole d&#39;ordine**

  Posizione dell’archivio di un nodo contenente il nodo predefinito `positive` e `negative` proprietà che specificano le parole d&#39;ordine predefinite. Il valore predefinito è `/libs/settings/community/watchwords/default`.

* **Regole di valutazione**

  Posizione dell’archivio delle regole per il calcolo della valutazione in base a parole d’ordine positive e negative. Il valore predefinito è `/libs/cq/workflow/components/workflow/social/sentiments/rules` (tuttavia, il flusso di lavoro non è più necessario).

Di seguito è riportato un esempio di voce personalizzata per le parole chiave predefinite, quando `Explicit Path to Watchwords Node` è impostato su `/libs/settings/community/watchwords/default`.

![crxde](assets/crxde.png)

### Autorizzazioni moderatore {#moderator-permissions}

Le seguenti autorizzazioni, se assegnate alla stessa risorsa, sono collettivamente denominate `moderator permissions`:

* `Read`
* `Modify`
* `Create`
* `Delete`
* `Replicate`
