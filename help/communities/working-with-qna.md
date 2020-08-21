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


# Funzionalità forum D e R{#q-a-forum-feature}

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
* Impostazioni di configurazione per il `QnA`componente.

## Aggiunta di un forum D e R a una pagina {#adding-a-q-a-forum-to-a-page}

Per aggiungere un `QnA` componente a una pagina in modalità di creazione, usate il browser Componenti per individuarlo `Communities / QnA` e trascinarlo nella posizione desiderata su una pagina in cui dovrebbe comparire il forum QnA.

Per le informazioni necessarie, consulta [Community Components Basics](/help/communities/basics.md).

Quando sono incluse le librerie [lato client](/help/communities/qna-essentials.md#essentials-for-client-side) richieste, viene visualizzato il `QnA` componente:

![qna-component](assets/qna-component.png)

### Configurazione di QnA {#configuring-qna}

Selezionate il `QnA` componente inserito a cui accedere e selezionate l’ `Configure` icona che apre la finestra di dialogo di modifica.

![configure](assets/configure-new.png)

![qna-config](assets/qna-config.png)

#### scheda Impostazioni {#settings-tab}

Nella scheda **Impostazioni** , specificate le impostazioni per gli argomenti (domande) e le risposte (risposte):

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

   Se questa opzione è selezionata, consentire ai membri di aggiungere etichette di tag al proprio post (consultate la scheda Campo **** tag ). Il valore predefinito è deselezionato.

* **Consenti caricamenti file**

   Se questa opzione è selezionata, consentire l&#39;aggiunta di allegati alla domanda o al commento. Il valore predefinito è deselezionato.

* **Consenti Segui**

   Se questa opzione è selezionata, includete la seguente funzione per i post del forum, che consente ai membri di ricevere [notifiche](/help/communities/notifications.md) sui nuovi post. Il valore predefinito è deselezionato.

* **Consenti blocco**

   Se questa opzione è attivata, gli argomenti del forum possono essere bloccati in cima all’elenco degli argomenti. Il valore predefinito è deselezionato.

* **Consenti iscrizioni e-mail**

   Se questa opzione è attivata, consentite ai membri di ricevere notifiche sui nuovi post via e-mail ([iscrizione](/help/communities/subscriptions.md)). Richiede che l’opzione Consenti seguito sia selezionata e che sia configurata [l’](/help/communities/email.md)e-mail. Il valore predefinito è deselezionato.

* **Dimensione file massima**

   Pertinente solo se `Allow File Uploads` è controllato. Questo campo limita la dimensione (in byte) di un file caricato. Il valore predefinito è 104857600 (10 Mb).

* **Tipi di file consentiti**

   Pertinente solo se `Allow File Uploads` è controllato. Un elenco separato da virgole di estensioni di file con il separatore &quot;punto&quot;. Ad esempio: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se vengono specificati dei tipi di file, non è consentito caricarli. Il valore predefinito non è specificato in modo che** **tutti i tipi di file siano consentiti.

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

   Se questa opzione è attivata, vengono visualizzati [i simboli](/help/communities/implementing-scoring.md) guadagnati e assegnati con il post di blog di un membro. Il valore predefinito è deselezionato.

* **Consenti contenuto in primo piano**

   se questa opzione è attivata, l’idea può essere identificata come contenuto [](/help/communities/featured.md)disponibile. Il valore predefinito è deselezionato.

* **Abilita menzione**

   Se abilitata, consente agli utenti della community registrati di identificare altri membri registrati (utilizzando nome, cognome, nome utente) e di assegnare loro un tag utilizzando la sintassi comune @user-name. Gli utenti con tag ricevono notifiche relative alle loro menzioni.

* **Max menzioni**

   Limita il numero massimo di menzioni consentite in un post. Il valore predefinito è 10.

* **Pattern menzioni interfaccia**

   Specificare la stringa di pattern consentita per assegnare un tag (@reference) all&#39;utente registrato in un post. Esempio, `~{{familyName}}{{givenName}}`.

#### Scheda Moderazione utente {#user-moderation-tab}

Nella scheda Moderazione **** utente, specificate in che modo vengono gestiti gli argomenti (domande) e le risposte (contenuto generato dall’utente) inviati. Per ulteriori informazioni, consultate [Moderazione del contenuto](/help/communities/moderate-ugc.md)generato dall&#39;utente.

* **Rifiuta risposte**

   Se questa opzione è attivata, i moderatori membri attendibili possono negare le risposte pubblicate e impedire che vengano visualizzate nel forum pubblico D e R. Il valore predefinito è deselezionato.

* **Chiudi/Riapri argomenti**

   Se questa opzione è attivata, i moderatori di membri attendibili possono chiudere una domanda (argomento) per apportare ulteriori modifiche e risposte, nonché riaprire una domanda. Il valore predefinito è deselezionato.

* **Sposta argomenti** Se questa opzione è selezionata, consente ai moderatori lato pubblicazione di spostare le domande. Il valore predefinito è deselezionato.

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

Nella scheda Campo **** tag, i tag che possono essere applicati, se consentiti nella scheda **Impostazioni** , sono limitati in base agli spazi dei nomi selezionati.

* **Namespace consentiti**

   Pertinente se `Allow Tagging` è selezionato sotto la scheda **Impostazioni** . I tag che possono essere applicati sono limitati a quelli all&#39;interno delle categorie dello spazio nomi selezionate. L&#39;elenco degli spazi dei nomi include &quot;Tag standard&quot; (lo spazio dei nomi predefinito) e &quot;Includi tutti i tag&quot;. Il valore predefinito non è selezionato, il che significa che tutti gli spazi dei nomi sono consentiti.

* **Limite di suggerimenti**

   Immettete il numero di tag da visualizzare come suggerimento al membro che invia il messaggio al forum. Un valore di **-**1 non indica limiti. Il valore predefinito è 0.

#### Scheda Impostazioni ordinamento {#sort-settings-tab}

Nella scheda **Impostazioni** ordinamento, specificare in che modo i commenti inviati vengono ordinati quando vengono visualizzati.

* **Ordina per**

   Seleziona tutte le selezioni di ordinamento consentite: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. Default is `Newest, Oldest, Last Updated`.

* **Imposta come predefinito**

   Estrai per selezionare una delle opzioni di ordinamento selezionate da visualizzare come predefinita. Default is `Newest`.

* **Seleziona le opzioni di tempo per l&#39;ordinamento Analytics**

   Rilasciate per selezionare uno dei `All, Last 24 Hours, Last 7 Days, Last 30 Days`. Default is `All`.

## Esperienza dei visitatori del sito {#site-visitor-experience}

### Identificazione delle risposte {#identifying-answers}

Una risposta può essere contrassegnata come una risposta corretta o utile utilizzando il `Select Answer` pulsante. Una volta che una domanda è contrassegnata come Risposta, non è possibile selezionare un&#39;altra risposta fino a quando la prima non è stata deselezionata utilizzando il `Unmark Chosen Answer` pulsante.

Una volta selezionata come risposta valida, è possibile deselezionarla utilizzando il `Unmark Chosen Answer` pulsante.

Una volta selezionata una risposta come risposta valida, l&#39;indicazione che la domanda è stata `Answered` visualizzata accanto all&#39;argomento della domanda nella pagina QnA principale.

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

Per la moderazione degli argomenti e dei commenti pubblicati, consultate [Moderazione del contenuto](/help/communities/moderate-ugc.md)generato dall&#39;utente.

Per assegnare tag agli argomenti e ai commenti inviati, consultate [Assegnazione di tag ai contenuti](/help/communities/tag-ugc.md)generati dagli utenti.
