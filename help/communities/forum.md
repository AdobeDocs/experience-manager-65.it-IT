---
title: Funzione forum
seo-title: Forum Feature
description: Aggiungere e configurare la funzione forum
seo-description: How to add and configure the forum feature
uuid: e69be4e1-c9d5-4d51-8e7e-609e5460e378
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d936cef5-ad76-482d-97bf-c40137185812
docset: aem65
exl-id: 2b1a4917-9db6-436a-a5fd-c102fe41fb9d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 10%

---

# Funzione forum{#forum-feature}

## Introduzione {#introduction}

La funzione forum fornisce un’area per i visitatori del sito con accesso (membri della community) nell’ambiente di pubblicazione per:

* Creazione di nuovi argomenti
* Visualizzare e rispondere agli argomenti
* Seguire un argomento
* Cercare un forum
* Aiutare a moderare il contenuto del forum
* Spostare gli argomenti del forum da una pagina all&#39;altra

Questa sezione della documentazione descrive:

* Aggiunta della funzione forum a un sito AEM.
* Impostazioni di configurazione per `Forum` componente.

### Aggiunta di un forum a una pagina {#adding-a-forum-to-a-page}

Per aggiungere una `Forum` componente per una pagina in modalità di creazione, usate il browser componenti per individuare

* `Communities / Forum`

e trascinarlo nella posizione desiderata su una pagina in cui dovrebbe essere visualizzato il forum.

Per le informazioni necessarie, visita [Nozioni di base sui componenti di Communities](/help/communities/basics.md).

Quando il [librerie lato client richieste](/help/communities/essentials-forum.md#essentials-for-client-side) sono inclusi, è così che `Forum` apparirà il componente:

![componente forum](assets/forum-component.png)

### Configurazione di un forum {#configuring-a-forum}

Seleziona il `Forum` per accedere e selezionare il `Configure` che apre la finestra di dialogo di modifica.

![configure-new](assets/configure-new.png)

![forum-config](assets/forum-config.png)

#### Scheda Impostazioni {#settings-tab}

Sotto la **Impostazioni** scheda , specifica le impostazioni per gli argomenti e le risposte:

* **Consenti miniatura allegato**

   Se questa opzione è selezionata, viene creata una miniatura dell&#39;immagine allegata.

* **Dimensione max miniatura allegato**

   Dimensione massima (in pixel) dell&#39;immagine miniatura dell&#39;allegato. Il valore predefinito è 800 x 800.

* **Dimensione minima dell&#39;immagine per la miniatura**
* **Dimensione massima miniatura**

   Dimensione massima (in pixel) dell&#39;immagine in miniatura per l&#39;immagine in linea. Il valore predefinito è 800 x 800.

* **Topic per pagina**

   Definisce il numero di topic/post mostrati per pagina. Impostazione predefinita: 10.

* **Moderato**

   Se questa opzione è selezionata, la pubblicazione di argomenti e commenti deve essere approvata prima che vengano visualizzati su un sito di pubblicazione. Il valore predefinito è deselezionato.

* **Chiuso**

   Se questa opzione è selezionata, il forum viene chiuso ai nuovi argomenti e commenti. Il valore predefinito è deselezionato.

* **Editor Rich Text**

   Se questa opzione è selezionata, è possibile inserire argomenti e commenti con markup. Il valore predefinito è deselezionato.

* **Consenti assegnazione tag**

   Se questa opzione è selezionata, consenti ai membri di aggiungere etichette di tag al proprio post (consulta **Campo tag** ). Il valore predefinito è deselezionato.

* **Consenti caricamenti file**

   Se questa opzione è selezionata, consenti l’aggiunta di allegati all’argomento o al commento. Il valore predefinito è deselezionato.

* **Consenti Segui**

   Se questa opzione è selezionata, includi la seguente funzione per i post del forum, che consente ai membri di essere [notificato](/help/communities/notifications.md) di nuovi posti. Il valore predefinito è deselezionato.

* **Consenti blocco**

   Se questa opzione è selezionata, gli argomenti del forum possono essere inseriti in cima all’elenco. Il valore predefinito è deselezionato.

* **Consenti contenuto in primo piano**

   Se questa opzione è selezionata, l’idea può essere identificata come [contenuto in primo piano](/help/communities/featured.md). Il valore predefinito è deselezionato.

* **Consenti iscrizioni e-mail**

   Se questa opzione è selezionata, consente ai membri di ricevere notifiche sui nuovi post via e-mail ([abbonamento](/help/communities/subscriptions.md)). Richiede `Allow Following` da controllare e [e-mail configurata](/help/communities/email.md). Il valore predefinito è deselezionato.

* **Dimensione file massima**

   Pertinente solo se `Allow File Uploads` è controllata. Questo campo limita le dimensioni (in byte) di un file caricato. Il valore predefinito è 104857600 (10 Mb).

* **Tipi di file consentiti**

   Pertinente solo se `Allow File Uploads` è controllata. Elenco di estensioni di file separate da virgola con il separatore &quot;punto&quot;. Ad esempio: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se sono specificati dei tipi di file, non sarà possibile caricare quelli non specificati. Il valore predefinito non è specificato in modo che tutti i tipi di file siano consentiti.

* **Dimensione massima file immagine allegato**
Pertinente solo se l’opzione Consenti caricamenti file è selezionata. Numero massimo di byte di un file immagine caricato. Il valore predefinito è 2097152 (2 Mb).

* **Consenti risposte concatenate**

   Se questa opzione è selezionata, consenti risposte ai commenti pubblicati nell&#39;argomento. Il valore predefinito è deselezionato.

* **Consenti votazione**

   Se questa opzione è selezionata, includi la funzionalità Voto con un argomento. Il valore predefinito è deselezionato.

* **Consenti agli utenti di eliminare commenti e argomenti**

   Se questa opzione è selezionata, consentire ai membri di eliminare i commenti e gli argomenti pubblicati. Il valore predefinito è deselezionato.

* **Mostra breadcrumb**

   Se questa opzione è selezionata, verranno visualizzate le breadcrumb di navigazione nelle pagine dell’argomento. Il valore predefinito è selezionato.

* **Visualizza badge**

   Se selezionato, visualizza guadagnato e assegnato [badge](/help/communities/implementing-scoring.md) con il post di blog di un membro. Il valore predefinito è deselezionato.

* **Consenti membri privilegiati**

   Se questa opzione è selezionata, solo i membri con privilegi possono creare contenuto.

* **Membri privilegiati consentiti**

   Aggiungi i membri con privilegi consentiti per creare contenuto.

* **Blocca i contenuti generati dagli utenti in modalità di modifica Creazione**

   Se attivato, blocca il contenuto generato dall’utente durante la modifica in modalità Autore.

* **Abilita menzione**

   Se attivato, consente agli utenti della community registrata di identificare altri membri registrati (utilizzando nome, cognome, nome utente) e di assegnare loro un tag utilizzando la comune sintassi @user-name. Gli utenti con tag ricevono notifiche sulle loro menzioni.

* **Max menzioni**

   Limita il numero massimo di menzioni consentite in un post. Il valore predefinito è 10.

* **Pattern menzioni interfaccia**

   Specifica la stringa di pattern consentita per assegnare il tag (@menzione) all’utente registrato in un post. Esempio `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Può essere necessario controllare entrambi `AllowThreaded Replies` e `Allow users to Delete Comments and Topics` per abilitare i commenti su un argomento.

#### Scheda Moderazione utente {#user-moderation-tab}

Sotto la **Moderazione utente** scheda , specifica come vengono gestiti gli argomenti e le risposte pubblicati (contenuto generato dall’utente). Per ulteriori informazioni, consulta [Moderazione dei contenuti generati dagli utenti](/help/communities/moderate-ugc.md).

* **Rifiuta post**

   Se questa opzione è selezionata, ai moderatori di membri affidabili sarà consentito di negare i post e impedire che il post appaia sul forum pubblico. Il valore predefinito è deselezionato.

* **Chiudi/Riapri argomenti**

   Se questa opzione è selezionata, i moderatori di membri attendibili possono chiudere un argomento per ulteriori modifiche e commenti e riaprire un argomento. Il valore predefinito è deselezionato.

* **Sposta argomenti**

   Se questa opzione è selezionata, consenti ai moderatori lato pubblicazione di spostare gli argomenti. Il valore predefinito è selezionato.

* **Segnala post**

   Se questa opzione è selezionata, consentire ai membri di contrassegnare gli argomenti o i commenti di altri come inappropriati. Il valore predefinito è deselezionato.

* **Elenco di motivi per segnalazione**

   Se questa opzione è selezionata, consenti ai membri di scegliere, da un elenco a discesa, il motivo per cui contrassegnano un argomento o un commento come inappropriato. Il valore predefinito è deselezionato.

* **Motivo per segnalazione personalizzato**

   Se questa opzione è selezionata, consenti ai membri di inserire il proprio motivo per contrassegnare un argomento o un commento come inappropriato. Il valore predefinito è deselezionato.

* **Soglia moderazione**

   Immettere il numero di volte in cui un argomento o un commento deve essere segnalato dai membri prima che i moderatori ne vengano informati. Il valore predefinito è 1 (una volta).

* **Limite segnalazione**

   Immetti il numero di volte in cui un argomento o un commento deve essere contrassegnato prima che sia nascosto dalla visualizzazione pubblica. Se è impostato su -1, l&#39;argomento o il commento contrassegnato non viene mai nascosto dalla visualizzazione pubblica. In caso contrario, questo numero deve essere maggiore o uguale alla soglia di moderazione. Il valore predefinito è 5.

#### Scheda Campo tag {#tag-field-tab}

Sotto la **Campo tag** , i tag che possono essere applicati, se consentiti nella **Impostazioni** sono limitati in base ai namespace selezionati.

* **Namespace consentiti**

   Pertinente se `Allow Tagging` è controllato sotto **Impostazioni** scheda . I tag che possono essere applicati sono limitati a quelli nelle categorie dello spazio dei nomi selezionate. L’elenco dei namespace include sia &quot;Tag standard&quot; (lo spazio dei nomi predefinito) che &quot;Includi tutti i tag&quot;. Il valore predefinito non è selezionato, il che significa che tutti i namespace sono consentiti.

* **Limite di suggerimenti**

   Immettere il numero di tag da visualizzare come suggerimento al membro che pubblica sul forum. Il valore predefinito è **-**1 (nessun limite).

#### Scheda Traduzione {#translation-tab}

Sotto la **Traduzione** Se la traduzione è abilitata per il sito community, la traduzione può essere impostata per tradurre l&#39;intero argomento o i post selezionati.

* **Traduci tutto**

   Se questa opzione è selezionata, il thread del forum viene tradotto nella lingua preferita dell&#39;utente. Il valore predefinito è deselezionato.

#### Scheda Impostazioni di ordinamento {#sort-settings-tab}

Sotto la **Impostazioni di ordinamento** specificare l&#39;ordine dei commenti inviati quando vengono visualizzati.

* **Ordina per**

   Seleziona tutte le selezioni di ordinamento consentite : `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. Il valore predefinito è `Newest, Oldest, Last Updated`.

* **Imposta come predefinito**

   Passa il mouse verso il basso per selezionare una delle opzioni di ordinamento selezionate da visualizzare come impostazione predefinita. Il valore predefinito è `Newest`.

* **Seleziona le opzioni di tempo per l&#39;ordinamento Analytics**

   Premi il mouse per selezionare una delle seguenti opzioni: `All, Last 24 Hours, Last 7 Days, Last 30 Days`.

   Il valore predefinito è `All`.

### Informazioni aggiuntive {#additional-information}

Per ulteriori informazioni, consulta [Nozioni di base sul forum](/help/communities/essentials-forum.md) per sviluppatori.

Per la moderazione degli argomenti e dei commenti pubblicati, vedi [Moderazione dei contenuti generati dagli utenti](/help/communities/moderate-ugc.md).

Per assegnare tag agli argomenti e ai commenti pubblicati, vedi [Assegnazione tag ai contenuti generati dagli utenti](/help/communities/tag-ugc.md).

Per la traduzione degli argomenti e dei commenti pubblicati, vedi [Traduzione di contenuti generati dagli utenti](/help/communities/translate-ugc.md).
