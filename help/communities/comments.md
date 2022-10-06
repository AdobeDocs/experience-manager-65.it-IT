---
title: Utilizzo dei commenti
seo-title: Using Comments
description: La funzione Commenti consente ai visitatori del sito che hanno effettuato l’accesso di condividere le proprie opinioni e conoscenze
seo-description: Comments feature lets signed-in site visitors share their opinions and knowledge
uuid: 40acd962-846c-483c-b789-aab3a7d2b31b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 216cfb3e-777e-4773-afba-749debdca000
docset: aem65
exl-id: 30baebd9-13c5-4fde-a494-85601abc32a5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 6%

---

# Utilizzo dei commenti {#using-comments}

## Introduzione {#introduction}

La funzione commenti viene utilizzata per consentire ai visitatori del sito (membri) che hanno effettuato l’accesso di condividere le loro opinioni e conoscenze sui contenuti del sito. Questa funzione è spesso già presente in altre funzioni, ma può essere aggiunta a qualsiasi sito web.

Il documento descrive:

* Aggiunta `Comments` a una pagina.
* Impostazioni di configurazione per `Comments` componente.

>[!NOTE]
>
>Pubblicazione anonima di un commento non supportata. I visitatori del sito devono registrarsi (diventare membro) e accedere per partecipare.

### Aggiunta di commenti a una pagina {#adding-comments-to-a-page}

Per aggiungere una `Comments` componente per una pagina in modalità di creazione, usate il browser componenti per individuare

* `Communities / Comments`

e trascinarlo nella posizione desiderata su una pagina, ad esempio una posizione relativa alla funzione in cui gli utenti possono commentare, o semplicemente nella parte inferiore della pagina.

Per le informazioni necessarie, visita [Nozioni di base sui componenti di Communities](/help/communities/basics.md).

Quando il [librerie lato client richieste](/help/communities/essentials-comments.md#essentials-for-client-side) sono inclusi, è così che `Comments` viene visualizzato il componente .

![componente commenti](assets/comments-component.png)

>[!NOTE]
>
>Solo uno `Comments` può esistere in una pagina. Tieni presente che diverse funzioni di Communities includono già commenti, come un blog, un calendario, un forum, QnA e recensioni.

### Configurazione dei commenti {#configuring-comments}

Seleziona il `Comments` per accedere e selezionare il `Configure` che apre la finestra di dialogo di modifica.

![icona configura](assets/configure.png)

![osservazioni](assets/commentssettings.png)

#### Scheda Commenti {#comments-tab}

Sotto la **Commenti** Specifica in che modo i commenti vengono immessi dai visitatori.

* **Consenti risposte**

   Se questa opzione è selezionata, consente ai membri di rispondere ai commenti esistenti. Il valore predefinito è deselezionato.

* **Commenti per pagina**

   Limita il numero di commenti visualizzati per pagina e il numero di risposte visualizzate. Il valore predefinito è 10.

* **Consenti caricamenti file**

   Se questa opzione è selezionata, l’opzione per caricare un file viene visualizzata con la casella di immissione testo. Il valore predefinito è deselezionato.

* **Dimensione file massima**

   Pertinente solo se l’opzione Consenti caricamenti file è selezionata. Questo valore limita le dimensioni del file caricato. Il limite predefinito è 10 MB.

* **Lunghezza massima messaggio**

   Numero massimo di caratteri che possono essere immessi nella casella di testo. Il valore predefinito è 4096 caratteri.

* **Tipi di file consentiti**

   Pertinente solo se l’opzione Consenti caricamenti file è selezionata. Elenco di estensioni di nomi di file separate da virgola con il separatore &quot;punto&quot;. Ad esempio: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se sono specificati tipi di file, questi non sono consentiti. Il valore predefinito non è specificato in modo che tutti i tipi di file siano consentiti.

* **Editor Rich Text**

   Se questa opzione è selezionata, i commenti vengono inseriti con un markup. Il valore predefinito è deselezionato.

* **Consenti votazione**

   Se questa opzione è selezionata, l’opzione per votare verso l’alto o verso il basso viene visualizzata con la casella di immissione testo. Il valore predefinito è deselezionato.

* **Consenti Segui**

   Se questa opzione è selezionata, consentire ai membri di seguire i commenti. Il valore predefinito è deselezionato.

* **Visualizza badge**

   Se questa opzione è selezionata, consenti la visualizzazione dei badge acquisiti e assegnati. Il valore predefinito è deselezionato.

#### Scheda Moderazione utente {#user-moderation-tab}

Sotto la **Moderazione utente** , specifica come vengono gestiti i commenti inviati. Per ulteriori informazioni, consulta [Moderazione dei contenuti generati dagli utenti](/help/communities/moderate-ugc.md).

* **Premoderazione**

   Se questa opzione è selezionata, i commenti devono essere approvati prima di essere visualizzati su un sito di pubblicazione. Il valore predefinito è deselezionato.

* **Elimina commenti**

   Se questa opzione è selezionata, il membro che ha pubblicato il commento potrà eliminarlo. Il valore predefinito è deselezionato.

* **Rifiuta commenti**

   Se questa opzione è selezionata, consentire ai moderatori di negare i commenti. Il valore predefinito è deselezionato.

* **Chiudi/Riapri commenti**

   Se questa opzione è selezionata, consenti ai moderatori di chiudere e riaprire i commenti. Il valore predefinito è deselezionato.

* **Segnala commenti**

   Se questa opzione è selezionata, consentire ai membri di contrassegnare i commenti come non appropriati. Il valore predefinito è deselezionato.

* **Elenco di motivi per segnalazione**

   Se questa opzione è selezionata, consenti ai membri di scegliere, da un elenco a discesa, il motivo per cui contrassegnano un commento come inappropriato. Il valore predefinito è deselezionato.

* **Motivo per segnalazione personalizzato**

   Se questa opzione è selezionata, consenti ai membri di inserire il proprio motivo per contrassegnare un commento come inappropriato. Il valore predefinito è deselezionato.

* **Soglia moderazione**

   Immettere il numero di volte in cui un commento deve essere contrassegnato dai membri prima che i moderatori vengano informati. Il valore predefinito è una tantum (1).

* **Limite segnalazione**

   Immetti il numero di volte in cui un commento deve essere contrassegnato prima che venga nascosto dalla visualizzazione pubblica. Questo numero deve essere maggiore o uguale a **Soglia moderazione**. Il valore predefinito è 5.

#### Scheda Impostazioni di ordinamento {#sort-settings-tab}

Sotto la **Impostazioni di ordinamento** specificare l&#39;ordine dei commenti inviati quando vengono visualizzati.

* **Campo di ordinamento**

   Abbassi per selezionare uno dei `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`oppure `Most Liked`.

* **Ordinamento**

   Abbassi per selezionare uno dei `Ascending` o `Descending`.

### Modifica a un tipo di commento personalizzato {#changing-to-a-custom-comment-type}

Modificando il tipo di risorsa commento, il sistema di commento non genera più un&#39;istanza di un commento utilizzando il valore predefinito, ma piuttosto un commento personalizzato (esteso) dagli sviluppatori.

Una volta noti i tipi di risorse personalizzati, immetti [Modalità Progettazione](/help/sites-authoring/default-components-designmode.md) e fai doppio clic su inserito `Comments` per aprire una finestra di dialogo con una scheda aggiuntiva.

Sotto la **Tipi di risorse** specifica il resourceType personalizzato per le nuove istanze del `Comments or Voting` componenti:

![tipo di risorsa](assets/resource-type.png)

* **Tipo risorsa commento**

   Passa al resourceType di un esteso `comment` componente (singolo commento) in /apps. Esempio, `/apps/social/commons/components/hbs/comments/comment`

   Questa risorsa identifica il resourceType dell&#39;UGC creato quando un visitatore pubblica un commento.

* **Tipo di risorsa per votazione**

   Passa al resourceType di un esteso `voting` in /apps. Esempio, `/apps/social/components/hbs/voting`

   Questa risorsa identifica il tipo di risorsa dell’UGC creato quando un visitatore pubblica un voto.

* **Tipo risorsa sistema di commenti**

   Passa al resourceType di un esteso `comments`componente (sistema di commenti) in /apps. Lascia vuoto a meno che il modello di pagina [include dinamicamente](/help/communities/scf.md#add-or-include-a-communities-component) il sistema di commenti nello script sottostante anziché essere aggiunto alla pagina come risorsa (nodo di commenti). Per saperne di più, leggi [{{include}} aiutante](/help/communities/handlebars-helpers.md#include).

### Esperienza dei visitatori del sito {#site-visitor-experience}

#### Moderatori e amministratori {#moderators-and-administrators}

Quando l’utente connesso dispone di privilegi di moderatore o amministratore, può eseguire le attività di moderazione consentite dalla configurazione del componente, indipendentemente da chi ha creato il commento.

#### Membri {#members}

Quando il visitatore del sito è connesso, a seconda della configurazione, può

* Pubblica un nuovo commento
* Modifica il proprio commento
* Elimina il proprio commento
* Contrassegna i commenti degli altri

#### Anonimo {#anonymous}

I visitatori del sito che non hanno effettuato l’accesso possono solo leggere i commenti postati, tradurli se supportati, ma non possono aggiungere un commento o contrassegnare i commenti degli altri.

### Informazioni aggiuntive {#additional-information}

Per ulteriori informazioni, consulta [Nozioni di base sui commenti](/help/communities/essentials-comments.md) per sviluppatori.

Per la moderazione dei commenti pubblicati, vedere [Moderazione dei contenuti generati dagli utenti](/help/communities/moderate-ugc.md).

Per la traduzione dei commenti pubblicati, consultare [Traduzione di contenuti generati dagli utenti](/help/communities/translate-ugc.md).
