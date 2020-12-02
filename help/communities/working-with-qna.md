---
title: Funzionalità forum D e R
seo-title: Funzionalità forum D e R
description: Aggiunta della funzione forum QnA a una pagina
seo-description: Aggiunta della funzione forum QnA a una pagina
uuid: e0d95009-0d04-4fa7-8d05-5948c4e37f08
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 6e6ffe09-c50b-4238-8b8c-597c133d0a9e
docset: aem65
translation-type: tm+mt
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 9%

---


# Funzione forum D e R{#q-a-forum-feature}

## Introduzione {#introduction}

La funzione di forum QnA (domande e risposte) offre ai membri della comunità l&#39;opportunità di porre e rispondere alle domande. Consente ai membri di:

* Creare nuove domande
* Aggiunta di immagini in linea (con supporto per trascinamento)
* Visualizzare e rispondere alle domande
* Ricerca di una domanda
* Aiutare a moderare il contenuto QnA
* Identificare le risposte migliori
* Spostare le domande QnA da una pagina all&#39;altra

La documentazione descrive:

* Aggiunta della funzione forum QnA a un sito AEM.
* Impostazioni di configurazione per il componente `QnA`.

## Aggiunta di un forum D e R a una pagina {#adding-a-q-a-forum-to-a-page}

Per aggiungere un componente `QnA` a una pagina in modalità di creazione, utilizzate il browser componenti per individuare `Communities / QnA` e trascinatelo nella posizione desiderata su una pagina in cui dovrebbe comparire il forum QnA.

Per le informazioni necessarie, visitare [Community Components Basics](/help/communities/basics.md).

Quando si includono le [librerie lato client ](/help/communities/qna-essentials.md#essentials-for-client-side), viene visualizzato il componente `QnA`:

![qna-component](assets/qna-component.png)

### Configurazione di QnA {#configuring-qna}

Selezionare il componente `QnA` inserito a cui accedere e selezionare l&#39;icona `Configure` che apre la finestra di dialogo di modifica.

![configure](assets/configure-new.png)

![qna-config](assets/qna-config.png)

#### Scheda Impostazioni {#settings-tab}

Nella scheda **Impostazioni**, specificate le impostazioni per gli argomenti (domande) e le risposte (risposte):

* **Consenti miniatura allegato**

   Se questa opzione è attivata, viene creata una miniatura dell’immagine allegata.

* **Dimensione max miniatura allegato**

   Dimensione massima (in pixel) dell’immagine della miniatura dell’allegato. Il valore predefinito è 800 x 800.

* **Dimensioni minime immagine per miniatura**

   Dimensione minima (in byte) dell&#39;immagine per la generazione della miniatura per le immagini in linea. Il valore predefinito è 100000 byte (100 kb).

* **Dimensione massima miniatura**

   Dimensione massima (in pixel) dell’immagine in miniatura per l’immagine agganciata. Il valore predefinito è 800 x 800.

* **Topic per pagina**

   Definisce il numero di domande/post mostrati per pagina. Il valore predefinito è 10.

* **Moderato**

   Se questa opzione è attivata, gli argomenti e i commenti devono essere approvati prima di essere visualizzati in un sito di pubblicazione. Il valore predefinito è deselezionato.

* **Chiuso**

   Se questa opzione è attivata, il forum è chiuso a nuove domande e commenti. Il valore predefinito è deselezionato.

* **Editor Rich Text**

   Se questa opzione è selezionata, è possibile inserire argomenti e commenti con la marcatura. Il valore predefinito è deselezionato.

* **Consenti assegnazione tag**

   Se questa opzione è selezionata, consentire ai membri di aggiungere etichette di tag al proprio post (vedere la scheda **Campo tag**). Il valore predefinito è deselezionato.

* **Consenti caricamenti file**

   Se questa opzione è selezionata, consentire l&#39;aggiunta di allegati alla domanda o al commento. Il valore predefinito è deselezionato.

* **Consenti Segui**

   Se questa opzione è selezionata, includete la seguente funzione per i post del forum, che consente ai membri di ricevere [notifiche](/help/communities/notifications.md) di nuovi post. Il valore predefinito è deselezionato.

* **Consenti blocco**

   Se questa opzione è attivata, gli argomenti del forum possono essere bloccati in cima all’elenco degli argomenti. Il valore predefinito è deselezionato.

* **Consenti iscrizioni e-mail**

   Se questa opzione è attivata, consentire ai membri di ricevere notifiche sui nuovi post via e-mail ([subscription](/help/communities/subscriptions.md)). Richiede l&#39;opzione Consenti l&#39;impostazione di quanto riportato di seguito e la configurazione di [e-mail](/help/communities/email.md). Il valore predefinito è deselezionato.

* **Dimensione file massima**

   Rilevante solo se è selezionato `Allow File Uploads`. Questo campo limita la dimensione (in byte) di un file caricato. Il valore predefinito è 104857600 (10 Mb).

* **Tipi di file consentiti**

   Rilevante solo se è selezionato `Allow File Uploads`. Un elenco separato da virgole di estensioni di file con il separatore &quot;punto&quot;. Ad esempio: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se vengono specificati dei tipi di file, non è consentito caricarli. Il valore predefinito non è specificato in modo che** **tutti i tipi di file siano consentiti.

* **Dimensione massima per file immagine allegato**

   Pertinente solo se l&#39;opzione Consenti caricamenti file è selezionata. Il numero massimo di byte che può contenere un file immagine caricato. Il valore predefinito è 2097152 (2 Mb).

* **Consenti risposte**

   Se questa opzione è selezionata, consentire le risposte ai commenti inviati alla domanda. Il valore predefinito è deselezionato.

* **Consenti votazione**

   Se questa opzione è selezionata, includete la funzione di votazione con una domanda. Il valore predefinito è deselezionato.

* **Consenti agli utenti di eliminare commenti e argomenti**

   Se questa opzione è selezionata, consentire ai membri di eliminare i commenti e le domande che hanno pubblicato. Il valore predefinito è deselezionato.

* **Consenti membri privilegiati**

   Se questa opzione è selezionata, solo i membri con privilegi possono creare contenuto.

* **Blocca i contenuti generati dagli utenti in modalità di modifica Creazione**

   Se attivato, blocca il contenuto generato dall&#39;utente durante la modifica in modalità Autore.

* **Porta in alto la risposta selezionata**

   Se questa opzione è attivata, la prima risposta visualizzata è una risposta selezionata. Il valore predefinito è deselezionato.
* **Visualizza badge**

   Se questa opzione è attivata, vengono visualizzati i simboli guadagnati e assegnati [con il post di blog di un membro. ](/help/communities/implementing-scoring.md) Il valore predefinito è deselezionato.

* **Consenti contenuto in primo piano**

   se questa opzione è attivata, l&#39;idea può essere identificata come [contenuto in evidenza](/help/communities/featured.md). Il valore predefinito è deselezionato.

* **Abilita menzione**

   Se abilitata, consente agli utenti della community registrati di identificare altri membri registrati (utilizzando nome, cognome, nome utente) e di assegnare loro un tag utilizzando la sintassi comune @user-name. Gli utenti con tag ricevono notifiche relative alle loro menzioni.

* **Max menzioni**

   Limita il numero massimo di menzioni consentite in un post. Il valore predefinito è 10.

* **Pattern menzioni interfaccia**

   Specificare la stringa di pattern consentita per assegnare un tag (@reference) all&#39;utente registrato in un post. Esempio, `~{{familyName}}{{givenName}}`.

#### Scheda Moderazione utente {#user-moderation-tab}

Nella scheda **Moderazione utente**, specificate in che modo vengono gestiti gli argomenti (domande) e le risposte (contenuto generato dall&#39;utente) inviati. Per ulteriori informazioni, vedere [Moderazione dei contenuti generati dall&#39;utente](/help/communities/moderate-ugc.md).

* **Rifiuta risposte**

   Se questa opzione è attivata, i moderatori membri attendibili possono negare le risposte pubblicate e impedire che vengano visualizzate nel forum pubblico D e R. Il valore predefinito è deselezionato.

* **Chiudi/Riapri argomenti**

   Se questa opzione è attivata, i moderatori di membri attendibili possono chiudere una domanda (argomento) per apportare ulteriori modifiche e risposte, nonché riaprire una domanda. Il valore predefinito è deselezionato.

* **Sposta**
argomenti: se questa opzione è selezionata, i moderatori lato pubblicazione possono spostare le domande. Il valore predefinito è deselezionato.

* **Segnala post**

   Se questa opzione è selezionata, consentire ai membri di contrassegnare le domande o le risposte di altri utenti in modo inappropriato. Il valore predefinito è deselezionato.

* **Elenco di motivi per segnalazione**

   Se questa opzione è selezionata, consentire ai membri di scegliere, da un elenco a discesa, il motivo per cui segnalano una domanda o una risposta come non appropriata. Il valore predefinito è deselezionato.

* **Motivo per segnalazione personalizzato**

   Se questa opzione è selezionata, consentire ai membri di inserire il proprio motivo per cui è stata segnalata una domanda o una risposta come inappropriata. Il valore predefinito è deselezionato.

* **Soglia moderazione**

   Immettete il numero di volte in cui i membri devono contrassegnare una domanda o una risposta prima che i moderatori ne vengano informati. Il valore predefinito è 1 (una volta).

* **Limite segnalazione**

   Immettete il numero di volte in cui una domanda o una risposta deve essere contrassegnata prima che venga nascosta dalla visualizzazione pubblica. Se è impostato su -1, la domanda o la risposta contrassegnata non viene mai nascosta dalla visualizzazione pubblica. In caso contrario, questo numero deve essere maggiore o uguale alla soglia di moderazione. Il valore predefinito è 5.

#### Scheda Campo tag {#tag-field-tab}

Nella scheda **Tag field** (Campo tag), i tag che possono essere applicati, se consentiti nella scheda **Settings** (Impostazioni), sono limitati in base agli spazi dei nomi scelti.

* **Namespace consentiti**

   Pertinente se `Allow Tagging` è selezionato nella scheda **Settings**. I tag che possono essere applicati sono limitati a quelli all&#39;interno delle categorie dello spazio nomi selezionate. L&#39;elenco degli spazi dei nomi include &quot;Tag standard&quot; (lo spazio dei nomi predefinito) e &quot;Includi tutti i tag&quot;. Il valore predefinito non è selezionato, il che significa che tutti gli spazi dei nomi sono consentiti.

* **Limite di suggerimenti**

   Immettete il numero di tag da visualizzare come suggerimento al membro che invia il messaggio al forum. Un valore di **-**1 non indica limiti. Il valore predefinito è 0.

#### Scheda Ordina impostazioni {#sort-settings-tab}

Nella scheda **Ordina impostazioni**, specificare in che modo i commenti inviati vengono ordinati quando vengono visualizzati.

* **Ordina per**

   Seleziona tutte le selezioni di ordinamento consentite: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. Il valore predefinito è `Newest, Oldest, Last Updated`.

* **Imposta come predefinito**

   Estrai per selezionare una delle opzioni di ordinamento selezionate da visualizzare come predefinita. Il valore predefinito è `Newest`.

* **Seleziona le opzioni di tempo per l&#39;ordinamento Analytics**

   Rilasciate per selezionare una delle `All, Last 24 Hours, Last 7 Days, Last 30 Days`. Il valore predefinito è `All`.

## Esperienza visitatori del sito {#site-visitor-experience}

### Identificazione delle risposte {#identifying-answers}

Una risposta può essere contrassegnata come una risposta corretta o utile utilizzando il pulsante `Select Answer`. Una volta che una domanda è contrassegnata come Risposta, non è possibile selezionare un&#39;altra risposta finché la prima non è stata deselezionata utilizzando il pulsante `Unmark Chosen Answer`.

Una volta selezionata come risposta valida, è possibile deselezionarla utilizzando il pulsante `Unmark Chosen Answer`.

Una volta selezionata una risposta come risposta valida, viene visualizzata un&#39;indicazione che la domanda è stata `Answered` accanto all&#39;argomento della domanda nella pagina QnA principale.

#### Moderatori e amministratori {#moderators-and-administrators}

Quando l’utente che ha effettuato l’accesso dispone di privilegi di moderatore o amministratore, può eseguire le attività di moderazione consentite dalla configurazione del componente, indipendentemente da chi ha creato la domanda o la risposta.

Possono anche identificare le risposte.

#### Membri {#members}

Quando i visitatori del sito hanno effettuato l’accesso, a seconda della configurazione, possono:

* Invia una nuova domanda.
* Modificate o eliminate le domande che hanno creato.
* Segnala domande o risposte di altri membri.
* Identificare le risposte alle domande che hanno creato.

#### Anonimo {#anonymous}

I visitatori del sito che non hanno effettuato l’accesso possono solo leggere le domande e le risposte pubblicate, tradurle se supportate, ma non possono aggiungere domande o risposte, né contrassegnare post di altri utenti.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [QnA Essentials](/help/communities/qna-essentials.md) per gli sviluppatori.

Per la moderazione degli argomenti e dei commenti pubblicati, vedere [Moderazione dei contenuti generati dall&#39;utente](/help/communities/moderate-ugc.md).

Per assegnare tag agli argomenti e ai commenti inviati, consultate [Assegnazione di tag ai contenuti generati dall&#39;utente](/help/communities/tag-ugc.md).
