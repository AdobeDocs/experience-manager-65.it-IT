---
title: Utilizzo dei commenti
description: La funzione Commenti consente ai visitatori del sito che hanno effettuato l’accesso di condividere le proprie opinioni e conoscenze
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 30baebd9-13c5-4fde-a494-85601abc32a5
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 1%

---

# Utilizzo dei commenti {#using-comments}

## Introduzione {#introduction}

La funzione commenti viene utilizzata per consentire ai visitatori del sito (membri) che hanno effettuato l’accesso di condividere le proprie opinioni e conoscenze relative al contenuto del sito. Questa funzione è spesso già presente in altre funzioni, ma può essere aggiunta a qualsiasi sito web.

Il documento descrive:

* Aggiunta di `Comments` a una pagina.
* Impostazioni di configurazione per il componente `Comments`.

>[!NOTE]
>
>La pubblicazione anonima di un commento non è supportata. I visitatori del sito devono registrarsi (diventare membri) e accedere per partecipare.

### Aggiunta di commenti a una pagina {#adding-comments-to-a-page}

Per aggiungere un componente `Comments` a una pagina in modalità di creazione, utilizza il browser componenti per individuare

* `Communities / Comments`

e trascinarlo nella posizione desiderata su una pagina, ad esempio una posizione relativa alla caratteristica su cui gli utenti possono commentare o semplicemente nella parte inferiore della pagina.

Per informazioni necessarie, visitare [Nozioni di base sui componenti delle community](/help/communities/basics.md).

Quando sono incluse le [librerie lato client richieste](/help/communities/essentials-comments.md#essentials-for-client-side), il componente `Comments` viene visualizzato in questo modo.

![commenti-componente](assets/comments-component.png)

>[!NOTE]
>
>In una pagina può esistere un solo componente `Comments`. Tieni presente che diverse funzioni di Communities includono già commenti, ad esempio blog, calendario, forum, domande e risposte e recensioni.

### Configurazione dei commenti {#configuring-comments}

Seleziona il componente `Comments` inserito a cui accedere e seleziona l&#39;icona `Configure` che apre la finestra di dialogo per modifica.

![icona di configurazione](assets/configure.png)

![impostazioni commenti](assets/commentssettings.png)

#### Scheda Commenti {#comments-tab}

Nella scheda **Commenti**, specifica come i commenti vengono immessi dai visitatori.

* **Consenti risposte**

  Se selezionato, consente ai membri di rispondere ai commenti esistenti. Il valore predefinito è deselezionato.

* **Commenti Per Pagina**

  Limita il numero di commenti visualizzati per pagina e il numero di risposte visualizzate. Il valore predefinito è 10.

* **Consenti caricamenti file**

  Se questa opzione è selezionata, l&#39;opzione per caricare un file viene visualizzata con la casella di immissione testo. Il valore predefinito è deselezionato.

* **Dimensione massima file**

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

* **Distintivi visualizzati**

  Se questa opzione è selezionata, consenti la visualizzazione dei distintivi ottenuti e aggiudicati. Il valore predefinito è deselezionato.

#### Scheda Moderazione utente {#user-moderation-tab}

Nella scheda **Moderazione utente**, specifica come vengono gestiti i commenti pubblicati. Per ulteriori informazioni, vedere [Moderazione del contenuto generato dall&#39;utente](/help/communities/moderate-ugc.md).

* **Pre-moderazione**

  Se questa opzione è selezionata, i commenti devono essere approvati prima di essere visualizzati in un sito pubblicato. Il valore predefinito è deselezionato.

* **Elimina commenti**

  Se questa opzione è selezionata, il membro che ha pubblicato il commento potrà eliminarlo. Il valore predefinito è deselezionato.

* **Rifiuta commenti**

  Se questa opzione è selezionata, consenti ai moderatori di rifiutare i commenti. Il valore predefinito è deselezionato.

* **Chiudi/Riapri commenti**

  Se questa opzione è selezionata, consenti ai moderatori di chiudere e riaprire i commenti. Il valore predefinito è deselezionato.

* **Contrassegna commenti**

  Se questa opzione è selezionata, consenti ai membri di segnalare i commenti non appropriati. Il valore predefinito è deselezionato.

* **Elenco motivi contrassegno**

  Se questa opzione è selezionata, consentire ai membri di scegliere, da un elenco a discesa, il motivo per cui contrassegnare un commento come non appropriato. Il valore predefinito è deselezionato.

* **Motivo contrassegno personalizzato**

  Se questa opzione è selezionata, consentire ai membri di immettere il proprio motivo per contrassegnare un commento come non appropriato. Il valore predefinito è deselezionato.

* **Soglia moderazione**

  Immetti il numero di volte in cui un commento deve essere segnalato dai membri prima che il moderatore riceva una notifica. Il valore predefinito è una tantum (1).

* **Limite di segnalazione**

  Immettere il numero di volte in cui un commento deve essere segnalato prima di essere nascosto alla visualizzazione pubblica. Questo numero deve essere maggiore o uguale alla **soglia di moderazione**. Il valore predefinito è 5.

#### Scheda Impostazioni ordinamento {#sort-settings-tab}

Nella scheda **Impostazioni ordinamento**, specifica l&#39;ordinamento dei commenti inviati quando vengono visualizzati.

* **Campo di ordinamento**

  Tirare verso il basso per selezionare uno di `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed` o `Most Liked`.

* **Ordinamento**

  Tirare verso il basso per selezionare uno di `Ascending` o `Descending`.

### Passaggio a un tipo di commento personalizzato {#changing-to-a-custom-comment-type}

Modificando il tipo di risorsa Commento, il sistema dei commenti non genera più un&#39;istanza di un commento utilizzando l&#39;impostazione predefinita, ma una che è stata personalizzata (estesa) dagli sviluppatori.

Una volta noti i tipi di risorse personalizzati, immetti [Modalità progettazione](/help/sites-authoring/default-components-designmode.md) e fai doppio clic sul componente `Comments` inserito per aprire una finestra di dialogo con una scheda aggiuntiva.

Nella scheda **Tipi di risorse**, specificare il tipo di risorsa personalizzato per le nuove istanze dei componenti `Comments or Voting`:

![tipo-risorsa](assets/resource-type.png)

* **Tipo risorsa commento**

  Passare a resourceType di un componente `comment` esteso (commento singolo) in /apps. Ad esempio `/apps/social/commons/components/hbs/comments/comment`

  Questa risorsa identifica il resourceType del UGC creato quando un visitatore pubblica un commento.

* **Tipo risorsa voto**

  Passare a resourceType di un componente `voting` esteso in /apps. Ad esempio `/apps/social/components/hbs/voting`

  Questa risorsa identifica il tipo di risorsa dell’UGC creato quando un visitatore pubblica un voto.

* **Tipo risorsa sistema commenti**

  Passare alla classe resourceType di un componente `comments` esteso (sistema di commenti) in /apps. Lasciare vuoto a meno che il modello di pagina [includa dinamicamente](/help/communities/scf.md#add-or-include-a-communities-component) il sistema di commenti nello script sottostante anziché essere aggiunto alla pagina come risorsa (nodo commenti). Ulteriori informazioni sull&#39;helper [`{{include}}`](/help/communities/handlebars-helpers.md#include).

### Esperienza visitatore del sito {#site-visitor-experience}

#### Moderatori e amministratori {#moderators-and-administrators}

Quando l&#39;utente connesso dispone dei privilegi di moderatore o amministratore, può eseguire le attività di moderazione consentite dalla configurazione del componente, indipendentemente da chi ha creato il commento.

#### Membri {#members}

Quando il visitatore del sito è connesso, a seconda della configurazione, potrebbe

* Post: un nuovo commento
* Modifica il proprio commento
* Elimina il proprio commento
* Contrassegna i commenti di altri utenti

#### Anonimo {#anonymous}

I visitatori del sito che non hanno effettuato l&#39;accesso possono solo leggere i commenti pubblicati, tradurli se supportati, ma non possono aggiungere un commento né contrassegnare i commenti di altri utenti.

### Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Comments Essentials](/help/communities/essentials-comments.md) per sviluppatori.

Per la moderazione dei commenti pubblicati, vedere [Moderazione del contenuto generato dall&#39;utente](/help/communities/moderate-ugc.md).

Per la traduzione dei commenti pubblicati, vedere [Traduzione del contenuto generato dall&#39;utente](/help/communities/translate-ugc.md).
