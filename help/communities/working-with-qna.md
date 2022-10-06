---
title: Funzione forum Q&A
seo-title: Q&A Forum Feature
description: Aggiunta della funzione forum QnA a una pagina
seo-description: Adding the QnA forum feature to a page
uuid: e0d95009-0d04-4fa7-8d05-5948c4e37f08
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 6e6ffe09-c50b-4238-8b8c-597c133d0a9e
docset: aem65
exl-id: 17081710-35e0-4f5b-9485-1f85c065fd70
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1368'
ht-degree: 9%

---

# Funzione forum Q&amp;A{#q-a-forum-feature}

## Introduzione {#introduction}

La funzione forum QnA (domande e risposte) offre ai membri della community un&#39;area in cui possono porre e rispondere a domande. Consente ai membri di:

* Crea nuove domande
* Aggiungi immagini in linea (con supporto per trascinamento)
* Visualizza e rispondi alle domande
* Cercare una domanda
* Aiutare a moderare il contenuto QnA
* Identificare le risposte migliori
* Sposta le domande di controllo qualità da una pagina all’altra

La documentazione descrive quanto segue:

* Aggiunta della funzione forum QnA a un sito AEM.
* Impostazioni di configurazione per `QnA`componente.

## Aggiunta di un forum di domande e risposte a una pagina {#adding-a-q-a-forum-to-a-page}

Per aggiungere una `QnA` componente per una pagina in modalità di creazione, usate il browser componenti per individuare `Communities / QnA` e trascinarlo nella posizione desiderata su una pagina in cui dovrebbe essere visualizzato il forum QnA.

Per le informazioni necessarie, visita [Nozioni di base sui componenti di Communities](/help/communities/basics.md).

Quando il [librerie lato client richieste](/help/communities/qna-essentials.md#essentials-for-client-side) sono inclusi, è così che `QnA` viene visualizzato il componente:

![qna-component](assets/qna-component.png)

### Configurazione di QnA {#configuring-qna}

Seleziona il `QnA` per accedere e selezionare il `Configure` che apre la finestra di dialogo di modifica.

![configurare](assets/configure-new.png)

![qna-config](assets/qna-config.png)

#### Scheda Impostazioni {#settings-tab}

Sotto la **Impostazioni** scheda , specifica le impostazioni per gli argomenti (domande) e le risposte (risposte):

* **Consenti miniatura allegato**

   Se questa opzione è selezionata, viene creata una miniatura dell&#39;immagine allegata.

* **Dimensione max miniatura allegato**

   Dimensione massima (in pixel) dell&#39;immagine miniatura dell&#39;allegato. Il valore predefinito è 800 x 800.

* **Dimensioni minime immagine per miniatura**

   Dimensione minima (in byte) dell&#39;immagine per la generazione di miniature per le immagini in linea. Il valore predefinito è 100000 byte (100 kb).

* **Dimensione massima miniatura**

   Dimensione massima (in pixel) dell&#39;immagine in miniatura per l&#39;immagine in linea. Il valore predefinito è 800 x 800.

* **Topic per pagina**

   Definisce il numero di domande/post visualizzati per pagina. Il valore predefinito è 10.

* **Moderato**

   Se questa opzione è selezionata, la pubblicazione di argomenti e commenti deve essere approvata prima che vengano visualizzati su un sito di pubblicazione. Il valore predefinito è deselezionato.

* **Chiuso**

   Se questa opzione è selezionata, il forum è chiuso a nuove domande e commenti. Il valore predefinito è deselezionato.

* **Editor Rich Text**

   Se questa opzione è selezionata, è possibile inserire argomenti e commenti con markup. Il valore predefinito è deselezionato.

* **Consenti assegnazione tag**

   Se questa opzione è selezionata, consenti ai membri di aggiungere etichette di tag al proprio post (consulta **Campo tag** ). Il valore predefinito è deselezionato.

* **Consenti caricamenti file**

   Se questa opzione è selezionata, consentire l&#39;aggiunta di allegati alla domanda o al commento. Il valore predefinito è deselezionato.

* **Consenti Segui**

   Se questa opzione è selezionata, includi la seguente funzione per i post del forum, che consente ai membri di essere [notificato](/help/communities/notifications.md) di nuovi posti. Il valore predefinito è deselezionato.

* **Consenti blocco**

   Se questa opzione è selezionata, gli argomenti del forum possono essere inseriti nella parte superiore dell’elenco. Il valore predefinito è deselezionato.

* **Consenti iscrizioni e-mail**

   Se questa opzione è selezionata, consente ai membri di ricevere notifiche sui nuovi post via e-mail ([abbonamento](/help/communities/subscriptions.md)). Richiede il controllo di Consenti di seguire e [e-mail configurata](/help/communities/email.md). Il valore predefinito è deselezionato.

* **Dimensione file massima**

   Pertinente solo se `Allow File Uploads` è controllata. Questo campo limita le dimensioni (in byte) di un file caricato. Il valore predefinito è 104857600 (10 Mb).

* **Tipi di file consentiti**

   Pertinente solo se `Allow File Uploads` è controllata. Elenco di estensioni di file separate da virgola con il separatore &quot;punto&quot;. Ad esempio: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se sono specificati tipi di file, non è possibile caricare quelli non specificati. Il valore predefinito non è specificato in modo che** **tutti i tipi di file siano consentiti.

* **Dimensione massima per file immagine allegato**

   Pertinente solo se l’opzione Consenti caricamenti file è selezionata. Il numero massimo di byte che può contenere un file immagine caricato. Il valore predefinito è 2097152 (2 Mb).

* **Consenti risposte**

   Se questa opzione è selezionata, consentire le risposte ai commenti inviati alla domanda. Il valore predefinito è deselezionato.

* **Consenti votazione**

   Se questa opzione è selezionata, includi la funzionalità di voto con una domanda. Il valore predefinito è deselezionato.

* **Consenti agli utenti di eliminare commenti e argomenti**

   Se questa opzione è selezionata, consentire ai membri di eliminare i commenti e le domande che hanno pubblicato. Il valore predefinito è deselezionato.

* **Consenti membri privilegiati**

   Se questa opzione è selezionata, solo i membri con privilegi possono creare contenuto.

* **Blocca i contenuti generati dagli utenti in modalità di modifica Creazione**

   Se attivato, blocca il contenuto generato dall’utente durante la modifica in modalità Autore.

* **Porta in alto la risposta selezionata**

   Se questa opzione è selezionata, la prima risposta visualizzata è una risposta selezionata. Il valore predefinito è deselezionato.
* **Visualizza badge**

   Se selezionato, visualizza guadagnato e assegnato [badge](/help/communities/implementing-scoring.md) con il post di blog di un membro. Il valore predefinito è deselezionato.

* **Consenti contenuto in primo piano**

   se questa opzione è selezionata, l’idea può essere identificata come [contenuto in primo piano](/help/communities/featured.md). Il valore predefinito è deselezionato.

* **Abilita menzione**

   Se attivato, consente agli utenti della community registrata di identificare altri membri registrati (utilizzando nome, cognome, nome utente) e di assegnare loro un tag utilizzando la comune sintassi @user-name. Gli utenti con tag ricevono notifiche sulle loro menzioni.

* **Max menzioni**

   Limita il numero massimo di menzioni consentite in un post. Il valore predefinito è 10.

* **Pattern menzioni interfaccia**

   Specifica la stringa di pattern consentita per assegnare il tag (@menzione) all’utente registrato in un post. Esempio: `~{{familyName}}{{givenName}}`.

#### Scheda Moderazione utente {#user-moderation-tab}

Sotto la **Moderazione utente** scheda , specifica come vengono gestiti gli argomenti pubblicati (domande) e le risposte (contenuto generato dall’utente). Per ulteriori informazioni, consulta [Moderazione dei contenuti generati dagli utenti](/help/communities/moderate-ugc.md).

* **Rifiuta risposte**

   Se questa opzione è selezionata, i moderatori di membri affidabili possono negare le risposte pubblicate e impedire che la risposta appaia sul forum Q&amp;A pubblico. Il valore predefinito è deselezionato.

* **Chiudi/Riapri argomenti**

   Se questa opzione è selezionata, i moderatori di membri affidabili possono chiudere una domanda (argomento) per ulteriori modifiche e risposte, nonché riaprire una domanda. Il valore predefinito è deselezionato.

* **Sposta argomenti**
Se questa opzione è selezionata, consenti ai moderatori lato pubblicazione di spostare le domande. Il valore predefinito è deselezionato.

* **Segnala post**

   Se questa opzione è selezionata, consentire ai membri di contrassegnare le domande o le risposte di altri utenti come inadeguate. Il valore predefinito è deselezionato.

* **Elenco di motivi per segnalazione**

   Se questa opzione è selezionata, consentire ai membri di scegliere, da un elenco a discesa, il motivo per cui contrassegnano una domanda o una risposta come inappropriata. Il valore predefinito è deselezionato.

* **Motivo per segnalazione personalizzato**

   Se questa opzione è selezionata, consentire ai membri di inserire il proprio motivo per contrassegnare una domanda o una risposta come inappropriata. Il valore predefinito è deselezionato.

* **Soglia moderazione**

   Immettere il numero di volte in cui una domanda o una risposta deve essere contrassegnata dai membri prima che i moderatori siano informati. Il valore predefinito è 1 (una volta).

* **Limite segnalazione**

   Immetti il numero di volte in cui una domanda o una risposta deve essere contrassegnata prima che sia nascosta dalla visualizzazione pubblica. Se è impostato su -1, la domanda o la risposta contrassegnata non viene mai nascosta dalla visualizzazione pubblica. In caso contrario, questo numero deve essere maggiore o uguale alla soglia di moderazione. Il valore predefinito è 5.

#### Scheda Campo tag {#tag-field-tab}

Sotto la **Campo tag** , i tag che possono essere applicati, se consentiti nella **Impostazioni** sono limitati in base ai namespace selezionati.

* **Namespace consentiti**

   Pertinente se `Allow Tagging` è controllato sotto **Impostazioni** scheda . I tag che possono essere applicati sono limitati a quelli nelle categorie dello spazio dei nomi selezionate. L’elenco degli spazi dei nomi include i tag standard (lo spazio dei nomi predefinito) e Includi tutti i tag. Il valore predefinito non è selezionato, il che significa che tutti i namespace sono consentiti.

* **Limite di suggerimenti**

   Immettere il numero di tag da visualizzare come suggerimento al membro che pubblica sul forum. Un valore di **-**1 non indica limiti. Il valore predefinito è 0.

#### Scheda Impostazioni di ordinamento {#sort-settings-tab}

Sotto la **Impostazioni di ordinamento** specificare l&#39;ordine dei commenti inviati quando vengono visualizzati.

* **Ordina per**

   Seleziona tutte le selezioni di ordinamento consentite: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. Il valore predefinito è `Newest, Oldest, Last Updated`.

* **Imposta come predefinito**

   Passa il mouse verso il basso per selezionare una delle opzioni di ordinamento selezionate da visualizzare come impostazione predefinita. Il valore predefinito è `Newest`.

* **Seleziona le opzioni di tempo per l&#39;ordinamento Analytics**

   Menu a discesa per selezionare uno dei `All, Last 24 Hours, Last 7 Days, Last 30 Days`. Il valore predefinito è `All`.

## Esperienza dei visitatori del sito {#site-visitor-experience}

### Identificazione delle risposte {#identifying-answers}

Una risposta può essere contrassegnata come risposta corretta o utile utilizzando `Select Answer` pulsante . Una volta che una domanda è contrassegnata come risposta, non è possibile selezionare un’altra risposta finché la prima non è stata deselezionata utilizzando la `Unmark Chosen Answer` pulsante .

Una volta selezionato come risposta valida, può essere deselezionato utilizzando la `Unmark Chosen Answer` pulsante .

Una volta che una risposta è stata selezionata come risposta valida, l&#39;indicazione che la domanda è stata `Answered` viene visualizzato accanto all’argomento della domanda nella pagina QnA principale.

#### Moderatori e amministratori {#moderators-and-administrators}

Quando l&#39;utente connesso dispone di privilegi di moderatore o amministratore, può eseguire le attività di moderazione consentite dalla configurazione del componente, indipendentemente da chi ha creato la domanda o la risposta.

Possono anche identificare le risposte.

#### Membri {#members}

Quando i visitatori del sito accedono, a seconda della configurazione, possono:

* Pubblica una nuova domanda.
* Modificare o eliminare le domande create.
* Contrassegna le domande o le risposte di altri membri.
* Identifica le risposte alle domande che hanno creato.

#### Anonimo {#anonymous}

I visitatori del sito che non hanno effettuato l’accesso possono solo leggere le domande e le risposte pubblicate, tradurle se supportate, ma non possono aggiungere domande o risposte, né contrassegnare post di altri.

## Informazioni aggiuntive {#additional-information}

Per ulteriori informazioni, consulta [Nozioni di base su QnA](/help/communities/qna-essentials.md) per sviluppatori.

Per la moderazione degli argomenti e dei commenti pubblicati, vedi [Moderazione dei contenuti generati dagli utenti](/help/communities/moderate-ugc.md).

Per assegnare tag agli argomenti e ai commenti pubblicati, vedi [Assegnazione tag ai contenuti generati dagli utenti](/help/communities/tag-ugc.md).
