---
title: Funzione forum domande e risposte
description: Scopri come aggiungere la funzione di forum di controllo qualità a una pagina che consente ai membri della community con accesso effettuato di porre e rispondere a domande.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 17081710-35e0-4f5b-9485-1f85c065fd70
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 0%

---

# Funzione forum domande e risposte{#q-a-forum-feature}

## Introduzione {#introduction}

La funzione del forum di QnA (domande e risposte) offre ai membri della community un’area in cui fare domande e rispondere. Consente ai membri di:

* Crea domande
* Aggiungi immagini in linea (con supporto per il trascinamento della selezione)
* Visualizza e rispondi alle domande
* Cerca una domanda
* Contribuire a moderare il contenuto QnA
* Identificare le risposte migliori
* Spostare le domande di controllo qualità da una pagina a un&#39;altra

La documentazione descrive:

* Aggiunta della funzione di forum di controllo qualità a un sito AEM.
* Impostazioni di configurazione per il componente `QnA`.

## Aggiunta di un forum domande e risposte a una pagina {#adding-a-q-a-forum-to-a-page}

Per aggiungere un componente `QnA` a una pagina in modalità di creazione, utilizzare il browser componenti per individuare `Communities / QnA` e trascinarlo in una pagina in cui dovrebbe apparire il forum QnA.

Per informazioni necessarie, visitare [Nozioni di base sui componenti delle community](/help/communities/basics.md).

Quando sono incluse le [librerie lato client richieste](/help/communities/qna-essentials.md#essentials-for-client-side), il componente `QnA` viene visualizzato in questo modo:

![qna-component](assets/qna-component.png)

### Configurazione di QnA {#configuring-qna}

Selezionare il componente `QnA` inserito in modo da poter accedere e selezionare l&#39;icona `Configure` che apre la finestra di dialogo per modifica.

![configura](assets/configure-new.png)

![qna-config](assets/qna-config.png)

#### Scheda Impostazioni {#settings-tab}

Nella scheda **Impostazioni**, specifica le impostazioni per gli argomenti (domande) e le risposte (risposte):

* **Consenti miniatura allegato**

  Se questa opzione è selezionata, viene creata una miniatura dell&#39;immagine allegata.

* **Dimensione massima miniatura allegato**

  Dimensione massima (in pixel) dell&#39;immagine miniatura dell&#39;allegato. Il valore predefinito è 800 x 800.

* **Dimensioni minime immagine per miniatura**

  Dimensione minima (in byte) dell&#39;immagine per la generazione della miniatura per le immagini in linea. Il valore predefinito è 100000 byte (100 kb).

* **Dimensione massima miniatura**

  Dimensione massima (in pixel) dell’immagine miniatura per l’immagine in linea. Il valore predefinito è 800 x 800.

* **Argomenti per pagina**

  Definisce il numero di domande/post mostrati per pagina. Il valore predefinito è 10.

* **Moderato**

  Se questa opzione è selezionata, è necessario approvare la pubblicazione di argomenti e commenti prima di visualizzarli in un sito pubblicato. Il valore predefinito è deselezionato.

* **Chiuso**

  Se questa opzione è selezionata, il forum non sarà accessibile a nuove domande e commenti. Il valore predefinito è deselezionato.

* **Editor Rich Text**

  Se questa opzione è selezionata, gli argomenti e i commenti possono essere immessi con il markup. Il valore predefinito è deselezionato.

* **Consenti assegnazione tag**

  Se questa opzione è selezionata, consentire ai membri di aggiungere etichette tag ai propri post (vedere la scheda **Campo tag**). Il valore predefinito è deselezionato.

* **Consenti caricamenti file**

  Se questa opzione è selezionata, consenti l&#39;aggiunta di file allegati alla domanda o al commento. Il valore predefinito è deselezionato.

* **Consenti Segui**

  Se questa opzione è selezionata, includere la funzionalità seguente per i post dei forum, che consente ai membri di ricevere [notifica](/help/communities/notifications.md) dei nuovi post. Il valore predefinito è deselezionato.

* **Consenti blocco**

  Se questa opzione è selezionata, gli argomenti del forum possono essere bloccati nella parte superiore dell&#39;elenco. Il valore predefinito è deselezionato.

* **Consenti iscrizioni e-mail**

  Se questa opzione è selezionata, consenti ai membri di ricevere notifiche sui nuovi post tramite e-mail ([abbonamento](/help/communities/subscriptions.md)). Richiede Consenti controllo dei seguenti elementi e [configurazione della posta elettronica](/help/communities/email.md). Il valore predefinito è deselezionato.

* **Dimensione massima file**

  Rilevante solo se è selezionato `Allow File Uploads`. Questo campo limita la dimensione (in byte) di un file caricato. Il valore predefinito è 104857600 (10 Mb).

* **Tipi di file consentiti**

  Rilevante solo se è selezionato `Allow File Uploads`. Un elenco separato da virgole di estensioni di file con il separatore &quot;punto&quot;. Ad esempio: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se sono specificati dei tipi di file, non è possibile caricare quelli non specificati. Il valore predefinito non è specificato in modo che siano consentiti **tutti** i tipi di file.

* **Dimensione massima file immagine allegato**

  Rilevante solo se è selezionata l’opzione Consenti caricamenti file. Il numero massimo di byte consentito per un file di immagine caricato. Il valore predefinito è 2097152 (2 Mb).

* **Consenti risposte**

  Se questa opzione è selezionata, consenti le risposte ai commenti inviati alla domanda. Il valore predefinito è deselezionato.

* **Consenti votazione**

  Se questa opzione è selezionata, includere la funzionalità Votazione con una domanda. Il valore predefinito è deselezionato.

* **Consenti agli utenti di eliminare commenti e argomenti**

  Se questa opzione è selezionata, consentire ai membri di eliminare i commenti e le domande pubblicati. Il valore predefinito è deselezionato.

* **Consenti membri privilegiati**

  Se questa opzione è selezionata, solo i membri con privilegi possono creare contenuto.

* **Blocca contenuto generato dall&#39;utente in modalità Modifica autore**

  Se questa opzione è abilitata, blocca i contenuti generati dagli utenti durante la modifica in modalità Creazione.

* **Sposta La Risposta Selezionata In Alto**

  Se questa opzione è selezionata, la prima risposta visualizzata è una risposta selezionata. Il valore predefinito è deselezionato.
* **Distintivi visualizzati**

  Se selezionato, visualizza i [distintivi](/help/communities/implementing-scoring.md) ottenuti e assegnati con il post di blog di un membro. Il valore predefinito è deselezionato.

* **Consenti contenuto in primo piano**

  Se questa opzione è selezionata, l&#39;idea è identificabile come [contenuto in primo piano](/help/communities/featured.md). Il valore predefinito è deselezionato.

* **Abilita menzione**

  Se questa opzione è attivata, consente agli utenti registrati della community di identificare altri membri registrati (tramite nome, cognome, nome utente) e di assegnare loro tag utilizzando la sintassi @user-name comune. Gli utenti taggati ricevono notifiche sulle loro menzioni.

* **Max menzioni**

  Limita il numero massimo di menzioni consentite in un post. Il valore predefinito è 10.

* **Pattern menzioni interfaccia utente**

  Specifica la stringa di pattern consentita per assegnare tag (@mention) all’utente registrato in un post. Esempio: `~{{familyName}}{{givenName}}`.

#### Scheda Moderazione utente {#user-moderation-tab}

Nella scheda **Moderazione utente**, specifica come vengono gestiti gli argomenti (domande) e le risposte (contenuti generati dall&#39;utente) pubblicati. Per ulteriori informazioni, vedere [Moderazione del contenuto generato dall&#39;utente](/help/communities/moderate-ugc.md).

* **Rifiuta risposte**

  Se questa opzione è selezionata, i moderatori dei membri di fiducia possono rifiutare le risposte pubblicate e impedirne la visualizzazione nel forum pubblico di domande e risposte. Il valore predefinito è deselezionato.

* **Chiudi/Riapri argomenti**

  Se questa opzione è selezionata, i moderatori membri attendibili possono chiudere una domanda (argomento) per ulteriori modifiche e risposte e riaprire una domanda. Il valore predefinito è deselezionato.

* **Sposta argomenti**
Se questa opzione è selezionata, consenti ai moderatori lato pubblicazione di spostare le domande. Il valore predefinito è deselezionato.

* **Contrassegna post**

  Se questa opzione è selezionata, consentire ai membri di segnalare le domande o le risposte di altri utenti come inappropriate. Il valore predefinito è deselezionato.

* **Elenco motivi contrassegno**

  Se questa opzione è selezionata, consentire ai membri di scegliere, da un elenco a discesa, il motivo per cui contrassegnare una domanda o una risposta come non appropriata. Il valore predefinito è deselezionato.

* **Motivo contrassegno personalizzato**

  Se questa opzione è selezionata, consentire ai membri di immettere il proprio motivo per contrassegnare una domanda o una risposta come non appropriata. Il valore predefinito è deselezionato.

* **Soglia moderazione**

  Immetti il numero di volte in cui i membri devono segnalare una domanda o una risposta prima che il moderatore riceva una notifica. Il valore predefinito è 1 (una tantum).

* **Limite di segnalazione**

  Immettere il numero di volte che una domanda o risposta deve essere contrassegnata prima che venga nascosta alla visualizzazione pubblica. Se è impostato su -1, la domanda o risposta contrassegnata non viene mai nascosta alla visualizzazione pubblica. Altrimenti, questo numero deve essere maggiore o uguale alla soglia di moderazione. Il valore predefinito è 5.

#### Scheda Campo tag {#tag-field-tab}

Nella scheda **Campo tag**, i tag che possono essere applicati, se consentiti nella scheda **Impostazioni**, sono limitati in base agli spazi dei nomi scelti.

* **Spazi dei nomi consentiti**

  Rilevante se `Allow Tagging` è selezionato nella scheda **Impostazioni**. I tag che possono essere applicati sono limitati a quelli all’interno delle categorie dello spazio dei nomi selezionate. L’elenco degli spazi dei nomi include &quot;Tag standard&quot; (lo spazio dei nomi predefinito) e &quot;Includi tutti i tag&quot;. L’impostazione predefinita non è selezionata, il che significa che tutti gli spazi dei nomi sono consentiti.

* **Limite suggerimenti**

  Immettere il numero di tag da visualizzare come suggerimento per la pubblicazione del membro nel forum. Il valore **-**1 indica nessun limite. Il valore predefinito è 0.

#### Scheda Impostazioni ordinamento {#sort-settings-tab}

Nella scheda **Impostazioni ordinamento**, specifica l&#39;ordinamento dei commenti inviati quando vengono visualizzati.

* **Ordina per**

  Controllare tutte le selezioni di ordinamento consentite: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. Il valore predefinito è `Newest, Oldest, Last Updated`.

* **Imposta come predefinito**

  Tirare verso il basso per selezionare una delle opzioni di ordinamento selezionate da visualizzare come impostazione predefinita. Il valore predefinito è `Newest`.

* **Selezionare le opzioni di tempo per l&#39;ordinamento di Analytics**

  Elenca a discesa per selezionare uno di `All, Last 24 Hours, Last 7 Days, Last 30 Days`. Il valore predefinito è `All`.

## Esperienza visitatore del sito {#site-visitor-experience}

### Identificazione delle risposte {#identifying-answers}

È possibile contrassegnare una risposta come corretta o utile utilizzando il pulsante `Select Answer`. Dopo aver contrassegnato una domanda come Risposta, è possibile selezionare un&#39;altra risposta solo dopo aver deselezionato la prima con il pulsante `Unmark Chosen Answer`.

Una volta selezionata come risposta valida, è possibile deselezionarla utilizzando il pulsante `Unmark Chosen Answer`.

Dopo aver selezionato una risposta come risposta valida, accanto all&#39;argomento della domanda nella pagina principale del Controllo di qualità viene visualizzata un&#39;indicazione che la domanda è stata `Answered`.

#### Moderatori e amministratori {#moderators-and-administrators}

Quando l&#39;utente connesso dispone dei privilegi di moderatore o amministratore, può eseguire le attività di moderazione consentite dalla configurazione del componente, indipendentemente da chi ha creato la domanda o la risposta.

Possono anche identificare le risposte.

#### Membri {#members}

Quando i visitatori del sito hanno effettuato l’accesso, a seconda della configurazione, possono:

* Post una nuova domanda.
* Modificare o eliminare le domande create.
* Contrassegna domande o risposte di altri membri.
* Identifica le risposte alle domande che hanno creato.

#### Anonimo {#anonymous}

I visitatori del sito che non hanno effettuato l&#39;accesso possono solo leggere le domande e le risposte pubblicate, tradurle se supportate, ma non possono aggiungere una domanda né rispondere, né segnalare i post di altri utenti.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [QnA Essentials](/help/communities/qna-essentials.md) per sviluppatori.

Per la moderazione degli argomenti e dei commenti pubblicati, vedere [Moderazione del contenuto generato dall&#39;utente](/help/communities/moderate-ugc.md).

Per assegnare tag agli argomenti e ai commenti pubblicati, vedere [Assegnazione di tag ai contenuti generati dagli utenti](/help/communities/tag-ugc.md).
