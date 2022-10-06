---
title: Moderazione dei contenuti della community
seo-title: Moderating Community Content
description: Concetti e azioni di moderazione
seo-description: Moderation concepts and actions
uuid: 5c991d3a-0037-4d78-8f91-bb62e44441fa
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6866d209-5789-4ef9-bc3c-d644d4fb4b1c
docset: aem65
role: Admin
exl-id: 22276580-e6bc-41c5-9ac3-e8f291f676b7
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 2%

---

# Moderazione dei contenuti della community {#moderating-community-content}

## Panoramica {#overview}

Il contenuto della community, noto anche come contenuto generato dall’utente (UGC), viene creato quando un membro (connesso al visitatore del sito) pubblica contenuto da un sito della community pubblicato tramite l’interazione con uno dei seguenti componenti della community :

* [Blog](/help/communities/blog-feature.md): i membri pubblicano un articolo o un commento sul blog.
* [Calendario](/help/communities/calendar.md): i membri pubblicano un evento calendario o un commento.
* [Commenti](/help/communities/comments.md): i membri pubblicano un commento o una risposta a un commento.

* [Forum](/help/communities/forum.md): i membri pubblicano un nuovo argomento o rispondono a un argomento.
* [Idea](/help/communities/ideation-feature.md): i membri pubblicano un&#39;idea o un commento.
* [QnA](/help/communities/working-with-qna.md): i membri creano una domanda o rispondono a una domanda.
* [Recensioni](/help/communities/reviews.md): i membri pubblicano un commento durante la valutazione di un elemento.

La moderazione dell&#39;UGC è utile per riconoscere i contributi positivi e limitare quelli negativi (come lo spam e il linguaggio abusivo). UGC può essere moderato da diversi ambienti:

* [Archiviazione dei contenuti comunitari](working-with-srp.md)

* [Console di moderazione in blocco](moderation.md)

   La console di moderazione è accessibile dagli amministratori e [moderatori della comunità](/help/communities/users.md) nell’ambiente pubblico e dagli amministratori dell’ambiente di authoring. Ciò è possibile quando il contenuto della community viene memorizzato in un [negozio comune](/help/communities/working-with-srp.md).

* [Moderazione nel contesto](in-context.md)

   La moderazione nell’ambiente di pubblicazione può essere eseguita da amministratori e moderatori della community direttamente nella pagina in cui è stato pubblicato il contenuto.

## Azioni di moderazione {#moderation-actions}

Le azioni che possono essere eseguite sul contenuto pubblicato (UGC) variano a seconda dell’identità dell’utente e dell’ambiente. La tabella seguente utilizza la seguente terminologia per descrivere i vari ruoli in base all’identità dell’utente :

* `Admin`

   Utente membro di [amministratori della community](users.md) gruppo.

* `Moderator`

   Un membro di un [moderatori della comunità](users.md#publishenvironmentusersandgroups) gruppo (ha [autorizzazioni del moderatore](in-context.md#moderatorpermissions)).

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
   <td><strong>Flag/<br /> Annulla flag</strong></td>
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

Dopo aver creato un post, questo può essere modificato o eliminato dal creatore, da un amministratore o da un moderatore della community.

Quando UGC viene eliminato, viene rimosso dall&#39;archivio e potrebbe non essere recuperato.

### Taglia {#cut}

Un amministratore o un moderatore della community può spostare uno o più argomenti del forum o domande di QnA da una posizione all’altra. Ciò include da un sito community a un altro sito community, purché lo stesso membro disponga di privilegi di moderazione su entrambi i siti.

Selezionando l’azione Taglia, il contenuto viene copiato negli Appunti. Più post possono essere copiati e spostati come gruppo nella nuova posizione.

![cutgc](assets/cutugc.png)

![putbackugc](assets/putbackugc.png)

Nell’altra posizione, quando il contenuto è presente negli Appunti, accanto a Nuovo post è visibile un pulsante Incolla con un numero che identifica il numero di post da incollare. Il pulsante Incolla include un’opzione per cancellare gli Appunti anziché incollarli.

![pastorizia](assets/pasteugc.png)

![pasteugc1](assets/pasteugc1.png)

### Rifiuta {#deny}

Un moderatore potrebbe impedire a UGC di rimanere visibile sul sito pubblicato. Per amministratori e moderatori della community, il post è ancora disponibile e viene annotato come spam.

### Chiudi/Riapri {#close-reopen}

L’azione Chiudi viene eseguita sull’intero thread della conversazione (un argomento del forum o il commento iniziale) e include tutti i post o le risposte successivi.

In caso di chiusura, non solo non sono possibili ulteriori risposte, ma non sono consentite nemmeno azioni di moderazione.

Per eseguire eventuali operazioni, è necessario riaprire l’argomento o il commento.

L&#39;azione Chiudi/Riapri può essere eseguita da amministratori o moderatori della community.

### Flag/Annulla flag {#flag-unflag}

Contrassegnare è un mezzo per qualsiasi membro connesso, ad eccezione del creatore del contenuto, per indicare che esiste un problema con il contenuto di un post. Una volta contrassegnata, viene visualizzata un’icona di rimozione dai flag che consente allo stesso membro di annullare la segnalazione del contenuto.

La moderazione nel contesto può essere configurata per consentire ai membri di selezionare un motivo quando si contrassegna un post. È possibile configurare l’elenco dei motivi dei flag selezionabili, specificando se è possibile immettere o meno un motivo personalizzato. Il motivo del flag viene salvato con l’UGC, ma il motivo non attiva alcuna azione particolare. Solo il numero di flag attiva una notifica. Il contenuto contrassegnato viene annotato come tale, in modo che i moderatori possano agirvi.

Il sistema tiene traccia di tutti i flag, che hanno segnalato, e del motivo del flag e invia un evento quando la soglia è stata raggiunta. Se l&#39;UGC è consentito da un moderatore della comunità, queste bandiere sono archiviate. Dopo l&#39;autorizzazione e l&#39;archiviazione, in caso di flaggings successivi, essi sarebbero archiviati come se non ci fossero stati flaggings precedenti.

### Consenti {#allow}

L’azione Consenti è un’opzione per UGC che è stata contrassegnata, negata o non è stata approvata in un sistema pre-moderato. L&#39;azione Consenti cancella qualsiasi stato contrassegnato o negato/spam presente e archivia tutti i dati contrassegnati.

## Concetti di moderazione comuni {#common-moderation-concepts}

### Premoderazione {#premoderation}

Quando UGC è premoderato, il post non apparirà sul sito pubblicato fino all&#39;approvazione da parte di un&#39;azione di moderazione. Durante la creazione di un [sito della community](/help/communities/sites-console.md), selezionando la casella [Contenuto sottoposto a moderazione](sites-console.md#moderation) consentirà la moderazione per l&#39;intero sito. Una volta inseriti i componenti in una pagina, i componenti che supportano la moderazione possono essere configurati per la moderazione utilizzando un’impostazione nella relativa finestra di dialogo di modifica:

* [Commenti](comments.md) e [recensioni](reviews.md)
in **[!UICONTROL Moderazione utente]** > **[!UICONTROL Pre-moderazione]**.

* [Forum](/help/communities/forum.md), [ideazione](/help/communities/ideation-feature.md), [QnA](/help/communities/working-with-qna.md)e [calendario](/help/communities/calendar.md)
in **[!UICONTROL Impostazioni]** > **[!UICONTROL Moderato]**.

### Rilevamento dello spam {#spam-detection}

Il rilevamento dello spam è una funzionalità di moderazione automatica che filtra i contenuti indesiderati generati dagli utenti inviati contrassegnandoli come spam. Una volta attivato, identifica se un contenuto generato dall’utente è spam o meno basato su una raccolta preconfigurata di parole spam. Le parole spam predefinite sono fornite in

`/libs/settings/community/sites/moderation/spamdetector-conf/profiles/spam_words.txt`.

Tuttavia, per personalizzare o estendere le parole spam predefinite, crea un set di parole nella directory /apps seguendo la struttura delle parole spam predefinite tramite [sovrapposizione](/help/communities/overlay-comments.md).

Un post generato dall&#39;utente (su tutti i tipi di contenuto, ad esempio blog, forum e commenti) contenente parole spam è contrassegnato con il testo &quot;Questo post è stato classificato come spam&quot; sopra il post.

Il moderatore può vedere un tale post e contrassegnare lo stesso per consentire o negare la visualizzazione sul sito. Le azioni di moderazione su questi post possono essere eseguite sia nel contesto che tramite l&#39;interfaccia utente di moderazione in blocco.

![spamdetection](assets/spamdetection.png)

Per abilitare il motore di rilevamento dello spam, segui questi passaggi:

1. Apri [Console web](https://localhost:4502/system/console/configMgr), andando `/system/console/configMgr`.

1. Individua **Moderazione automatica di AEM Communities** e modificalo.
1. Aggiungi il **[!UICONTROL SpamProcess]** voce.

![spam](assets/spamprocess.png)

>[!NOTE]
>
>Il rilevamento dello spam è implementato solo per le impostazioni internazionali inglesi.

### Sentimento {#sentiment}

Il sentimento è calcolato in base al numero di parole chiave positive e negative ([parole d&#39;ordine](#configuringwatchwords)) presente in un post (UGC).

L’analisi del sentiment utilizza un set di regole preconfigurate e calcola il sentimento dell’UGC. Le regole predefinite si trovano in: `/libs/cq/workflow/components/workflow/social/sentiments/rules.`

Il valore generato dalle regole è compreso tra 1 (tutte le parole negative, nessuna parola positiva) e 10 (tutte positive, nessuna parola negativa). Un valore del sentimento pari a 5 è un sentimento neutrale ed è il valore predefinito.

Le regole definite nel componente /libs sono:

* Articolo 1: imposta il valore su 1 se non ci sono parole positive e almeno una parola negativa.
* Articolo 2: imposta il valore su 10 se non ci sono parole negative e almeno una parola positiva.
* Articolo 3: imposta il valore su 3 se ci sono più parole negative che parole positive.
* Articolo 4: imposta il valore su 8 se ci sono più parole positive che parole negative.

Per sovrascrivere o aggiungere regole, crea un set di regole nella directory /apps seguendo la struttura delle regole predefinite. Modifica la configurazione del sentiment per identificare la posizione delle regole.

Una volta analizzato, il sentimento è memorizzato con l&#39;UGC.

Da [console di moderazione di gruppo](/help/communities/moderation.md), è possibile filtrare e visualizzare UGC in base al fatto che il sentimento sia negativo, neutro o positivo.

#### Parole da guardia {#watchwords}

AEM community fornisce *analizzatore di parole d&#39;ordine* come fase del processo di valutazione [sentimento](#sentiment). Il contributo al valore del sentiment fornito dalle parole d&#39;ordine è dovuto a un confronto tra parole d&#39;ordine negative e positive utilizzate nel contenuto pubblicato, così come le parole proibite.

#### Configurare sentiment e parole di controllo {#configure-sentiment-and-watchwords}

L&#39;elenco delle parole d&#39;ordine positive e negative può essere personalizzato come possono essere le regole del sentiment.

L&#39;elenco predefinito delle parole da guardare può essere immesso come proprietà di un nodo nel repository, simile al predefinito o ignorando il predefinito configurando il servizio OSGi `sentimentprocess.name` con l&#39;elenco delle parole.

La **sentimentprocess.name** può anche essere modificato per fare riferimento alla posizione di un set personalizzato di regole del sentiment.

Per configurare sentiment e watchwords:

* Accedi all’istanza di authoring come amministratore.
* Apri [Console web](https://localhost:4502/system/console/configMgr).
* Individua `sentimentprocess.name`.
* Seleziona la configurazione da aprire in modalità di modifica.

![sentimentale](assets/sentimentprocess.png)

* **Parole di controllo positive**

   Un elenco separato da virgole di parole che contribuiscono a un sentimento positivo che sovrascrive i valori predefiniti. Il valore predefinito è un elenco vuoto.

* **Parole di controllo negative**

   Un elenco separato da virgole di parole che contribuiscono a un sentimento negativo che sovrascrive i valori predefiniti. Il valore predefinito è un elenco vuoto.

* **Percorso esplicito al nodo Watchwords**

   Posizione del repository di un nodo contenente il valore predefinito `positive` e `negative` proprietà che specificano le parole d&#39;ordine predefinite. Il valore predefinito è `/libs/settings/community/watchwords/default`.

* **Regole sentiment**

   Posizione dell’archivio delle regole per il calcolo del sentiment basato su parole d’ordine positive e negative. Il valore predefinito è `/libs/cq/workflow/components/workflow/social/sentiments/rules` (tuttavia, non vi è più alcun flusso di lavoro coinvolto).

Di seguito è riportato un esempio di una voce personalizzata per le parole d’ordine predefinite, quando `Explicit Path to Watchwords Node` è impostato su `/libs/settings/community/watchwords/default`.

![crxde](assets/crxde.png)

### Autorizzazioni moderatore {#moderator-permissions}

Quando vengono assegnate alla stessa risorsa, le seguenti autorizzazioni vengono definite collettivamente `moderator permissions`:

* `Read`
* `Modify`
* `Create`
* `Delete`
* `Replicate`
