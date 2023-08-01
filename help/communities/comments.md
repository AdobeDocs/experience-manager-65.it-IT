---
title: Utilizzo dei commenti
description: La funzione Commenti consente ai visitatori del sito che hanno effettuato l’accesso di condividere le proprie opinioni e conoscenze
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 30baebd9-13c5-4fde-a494-85601abc32a5
source-git-commit: c667a1658e43bb5b61daede5f94256dae582a4fc
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 6%

---

# Utilizzo dei commenti {#using-comments}

## Introduzione {#introduction}

La funzione commenti viene utilizzata per consentire ai visitatori del sito (membri) che hanno effettuato l’accesso di condividere le proprie opinioni e conoscenze relative al contenuto del sito. Questa funzione è spesso già presente in altre funzioni, ma può essere aggiunta a qualsiasi sito web.

Il documento descrive:

* Aggiunta `Comments` a una pagina.
* Impostazioni di configurazione per `Comments` componente.

>[!NOTE]
>
>La pubblicazione anonima di un commento non è supportata. I visitatori del sito devono registrarsi (diventare membri) e accedere per partecipare.

### Aggiunta di commenti a una pagina {#adding-comments-to-a-page}

Per aggiungere una `Comments` a una pagina in modalità di authoring, utilizza il browser Componenti per individuare

* `Communities / Comments`

e trascinarlo nella posizione desiderata su una pagina, ad esempio una posizione relativa alla caratteristica su cui gli utenti possono commentare o semplicemente nella parte inferiore della pagina.

Per informazioni necessarie, visitare il sito [Nozioni di base sui componenti community](/help/communities/basics.md).

Quando [librerie lato client richieste](/help/communities/essentials-comments.md#essentials-for-client-side) sono inclusi, è così che `Comments` viene visualizzato.

![comments-component](assets/comments-component.png)

>[!NOTE]
>
>Solo uno `Comments` un componente può esistere in una pagina. Tieni presente che diverse funzioni di Communities includono già commenti, ad esempio blog, calendario, forum, domande e risposte e recensioni.

### Configurazione dei commenti {#configuring-comments}

Seleziona la inserita `Comments` per accedere e selezionare il `Configure` che apre la finestra di dialogo per modifica.

![icona configura](assets/configure.png)

![impostazionicommenti](assets/commentssettings.png)

#### Scheda Commenti {#comments-tab}

Sotto **Commenti** , specificare la modalità di immissione dei commenti da parte dei visitatori.

* **Consenti risposte**

  Se selezionato, consente ai membri di rispondere ai commenti esistenti. Il valore predefinito è deselezionato.

* **Commenti per pagina**

  Limita il numero di commenti visualizzati per pagina e il numero di risposte visualizzate. Il valore predefinito è 10.

* **Consenti caricamenti file**

  Se questa opzione è selezionata, l&#39;opzione per caricare un file viene visualizzata con la casella di immissione testo. Il valore predefinito è deselezionato.

* **Dimensione file massima**

  Rilevante solo se è selezionata l’opzione Consenti caricamenti file. Questo valore limita la dimensione del file caricato. Il limite predefinito è 10 MB.

* **Lunghezza massima messaggio**

  Numero massimo di caratteri che possono essere immessi nella casella di testo. Il valore predefinito è 4096 caratteri.

* **Tipi di file consentiti**

  Rilevante solo se è selezionata l’opzione Consenti caricamenti file. Un elenco separato da virgole di estensioni di file con il separatore &quot;punto&quot;. Ad esempio: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se sono specificati tipi di file, quelli non specificati non sono consentiti. Il valore predefinito è none specificato, pertanto tutti i tipi di file sono consentiti.

* **Editor Rich Text**

  Se questa opzione è selezionata, i commenti vengono immessi con il markup. Il valore predefinito è deselezionato.

* **Consenti votazione**

  Se questa opzione è selezionata, l&#39;opzione per votare verso l&#39;alto o verso il basso viene visualizzata con la casella di immissione testo. Il valore predefinito è deselezionato.

* **Consenti Segui**

  Se questa opzione è selezionata, consentire ai membri di seguire i commenti. Il valore predefinito è deselezionato.

* **Visualizza badge**

  Se questa opzione è selezionata, consenti la visualizzazione dei distintivi ottenuti e aggiudicati. Il valore predefinito è deselezionato.

#### Scheda Moderazione utente {#user-moderation-tab}

Sotto **Moderazione utenti** , specificare la modalità di gestione dei commenti pubblicati. Per ulteriori informazioni, consulta [Moderazione dei contenuti generati dagli utenti](/help/communities/moderate-ugc.md).

* **Premoderazione**

  Se questa opzione è selezionata, i commenti devono essere approvati prima di essere visualizzati in un sito pubblicato. Il valore predefinito è deselezionato.

* **Elimina commenti**

  Se questa opzione è selezionata, il membro che ha pubblicato il commento potrà eliminarlo. Il valore predefinito è deselezionato.

* **Rifiuta commenti**

  Se questa opzione è selezionata, consenti ai moderatori di rifiutare i commenti. Il valore predefinito è deselezionato.

* **Chiudi/Riapri commenti**

  Se questa opzione è selezionata, consenti ai moderatori di chiudere e riaprire i commenti. Il valore predefinito è deselezionato.

* **Segnala commenti**

  Se questa opzione è selezionata, consenti ai membri di segnalare i commenti non appropriati. Il valore predefinito è deselezionato.

* **Elenco di motivi per segnalazione**

  Se questa opzione è selezionata, consentire ai membri di scegliere, da un elenco a discesa, il motivo per cui contrassegnare un commento come non appropriato. Il valore predefinito è deselezionato.

* **Motivo per segnalazione personalizzato**

  Se questa opzione è selezionata, consentire ai membri di immettere il proprio motivo per contrassegnare un commento come non appropriato. Il valore predefinito è deselezionato.

* **Soglia moderazione**

  Immetti il numero di volte in cui un commento deve essere segnalato dai membri prima che il moderatore riceva una notifica. Il valore predefinito è una tantum (1).

* **Limite segnalazione**

  Immettere il numero di volte in cui un commento deve essere segnalato prima di essere nascosto alla visualizzazione pubblica. Questo numero deve essere maggiore o uguale al **Soglia moderazione**. Il valore predefinito è 5.

#### Scheda Impostazioni ordinamento {#sort-settings-tab}

Sotto **Impostazioni di ordinamento** , specificare l&#39;ordinamento dei commenti inviati quando vengono visualizzati.

* **Campo di ordinamento**

  Tirare verso il basso per selezionare uno dei `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`, o `Most Liked`.

* **Ordinamento**

  Tirare verso il basso per selezionare uno dei `Ascending` o `Descending`.

### Passaggio a un tipo di commento personalizzato {#changing-to-a-custom-comment-type}

Modificando il tipo di risorsa Commento, il sistema dei commenti non genera più un&#39;istanza di un commento utilizzando l&#39;impostazione predefinita, ma una che è stata personalizzata (estesa) dagli sviluppatori.

Una volta noti i tipi di risorse personalizzati, immetti [Modalità Progettazione](/help/sites-authoring/default-components-designmode.md) e fare doppio clic sul `Comments` per aprire una finestra di dialogo con una scheda aggiuntiva.

Sotto **Tipi di risorse** , specificare il resourceType personalizzato per le nuove istanze del `Comments or Voting` componenti:

![tipo-risorsa](assets/resource-type.png)

* **Tipo risorsa commento**

  Passare al resourceType di un&#39;estensione `comment` componente (commento singolo) in /apps. Ad esempio `/apps/social/commons/components/hbs/comments/comment`

  Questa risorsa identifica il resourceType del UGC creato quando un visitatore pubblica un commento.

* **Tipo di risorsa per votazione**

  Passare al resourceType di un&#39;estensione `voting` componente in /apps. Ad esempio `/apps/social/components/hbs/voting`

  Questa risorsa identifica il tipo di risorsa dell’UGC creato quando un visitatore pubblica un voto.

* **Tipo risorsa sistema commenti**

  Passare al resourceType di un&#39;estensione `comments`componente (sistema di commenti) in /apps. Lascia vuoto a meno che il modello della pagina non sia [include in modo dinamico](/help/communities/scf.md#add-or-include-a-communities-component) il sistema di commenti nello script sottostante, anziché essere aggiunto alla pagina come risorsa (nodo commenti). Per saperne di più leggi le [`{{include}}` aiutante](/help/communities/handlebars-helpers.md#include).

### Esperienza visitatore del sito {#site-visitor-experience}

#### Moderatori e amministratori {#moderators-and-administrators}

Quando l&#39;utente connesso dispone dei privilegi di moderatore o amministratore, può eseguire le attività di moderazione consentite dalla configurazione del componente, indipendentemente da chi ha creato il commento.

#### Membri {#members}

Quando il visitatore del sito è connesso, a seconda della configurazione, potrebbe

* Pubblica un nuovo commento
* Modifica il proprio commento
* Elimina il proprio commento
* Contrassegna i commenti di altri utenti

#### Anonimo {#anonymous}

I visitatori del sito che non hanno effettuato l&#39;accesso possono solo leggere i commenti pubblicati, tradurli se supportati, ma non possono aggiungere un commento né contrassegnare i commenti di altri utenti.

### Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili sul sito [Commenti essenziali](/help/communities/essentials-comments.md) pagina per sviluppatori.

Per la moderazione dei commenti pubblicati, vedi [Moderazione dei contenuti generati dagli utenti](/help/communities/moderate-ugc.md).

Per la traduzione dei commenti pubblicati, vedi [Traduzione dei contenuti generati dagli utenti](/help/communities/translate-ugc.md).
