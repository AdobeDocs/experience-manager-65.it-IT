---
title: Funzione forum
seo-title: Funzione forum
description: Come aggiungere e configurare la funzione forum
seo-description: Come aggiungere e configurare la funzione forum
uuid: e69be4e1-c9d5-4d51-8e7e-609e5460e378
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d936cef5-ad76-482d-97bf-c40137185812
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 10%

---


# Funzione forum{#forum-feature}

## Introduzione {#introduction}

La funzione forum fornisce un’area per i visitatori del sito che hanno effettuato l’accesso (membri della community) nell’ambiente di pubblicazione per:

* Creazione di nuovi argomenti
* Visualizzazione e risposta agli argomenti
* Seguire un argomento
* Ricerca in un forum
* Aiutare a moderare il contenuto del forum
* Spostare gli argomenti dei forum da una pagina all’altra

Questa sezione della documentazione descrive quanto segue:

* Aggiunta della funzione forum a un sito AEM.
* Impostazioni di configurazione per il componente `Forum`.

### Aggiunta di un forum a una pagina {#adding-a-forum-to-a-page}

Per aggiungere un componente `Forum` a una pagina in modalità di creazione, usate il browser componenti per individuare

* `Communities / Forum`

trascinatelo nella posizione desiderata su una pagina in cui dovrebbe essere visualizzato il forum.

Per le informazioni necessarie, visitare [Community Components Basics](/help/communities/basics.md).

Quando vengono incluse le [librerie lato client ](/help/communities/essentials-forum.md#essentials-for-client-side), viene visualizzato il componente `Forum`:

![chlimage_1-60](assets/chlimage_1-60.png)

### Configurazione di un forum {#configuring-a-forum}

Selezionare il componente `Forum` inserito a cui accedere e selezionare l&#39;icona `Configure` che apre la finestra di dialogo di modifica.

![chlimage_1-61](assets/chlimage_1-61.png)

![forum-config](assets/forum-config.png)

#### Scheda Impostazioni {#settings-tab}

Nella scheda **Impostazioni**, specificare le impostazioni per gli argomenti e le risposte:

* **Consenti miniatura allegato**

   Se questa opzione è attivata, viene creata una miniatura dell’immagine allegata.

* **Dimensione max miniatura allegato**

   Dimensione massima (in pixel) dell’immagine della miniatura dell’allegato. Il valore predefinito è 800 x 800.

* **Dimensione minima immagine per miniatura**
* **Dimensione massima miniatura**

   Dimensione massima (in pixel) dell’immagine in miniatura per l’immagine in linea. Il valore predefinito è 800 x 800.

* **Topic per pagina**

   Definisce il numero di topic/post mostrati per pagina. Impostazione predefinita: 10.

* **Moderato**

   Se questa opzione è attivata, gli argomenti e i commenti devono essere approvati prima che vengano visualizzati su un sito di pubblicazione. Il valore predefinito è deselezionato.

* **Chiuso**

   Se questa opzione è attivata, il forum è chiuso a nuovi argomenti e commenti. Il valore predefinito è deselezionato.

* **Editor Rich Text**

   Se questa opzione è selezionata, è possibile inserire argomenti e commenti con la marcatura. Il valore predefinito è deselezionato.

* **Consenti assegnazione tag**

   Se questa opzione è selezionata, consentire ai membri di aggiungere etichette di tag al proprio post (vedere la scheda **Campo tag**). Il valore predefinito è deselezionato.

* **Consenti caricamenti file**

   Se questa opzione è selezionata, consentire l&#39;aggiunta di allegati all&#39;argomento o al commento. Il valore predefinito è deselezionato.

* **Consenti Segui**

   Se questa opzione è selezionata, includete la seguente funzione per i post del forum, che consente ai membri di ricevere [notifiche](/help/communities/notifications.md) di nuovi post. Il valore predefinito è deselezionato.

* **Consenti blocco**

   Se questa opzione è attivata, gli argomenti del forum possono essere bloccati in cima all’elenco degli argomenti. Il valore predefinito è deselezionato.

* **Consenti contenuto in primo piano**

   Se questa opzione è selezionata, l&#39;idea può essere identificata come [contenuto in evidenza](/help/communities/featured.md). Il valore predefinito è deselezionato.

* **Consenti iscrizioni e-mail**

   Se questa opzione è attivata, consentire ai membri di ricevere notifiche sui nuovi post via e-mail ([subscription](/help/communities/subscriptions.md)). È necessario che `Allow Following` sia selezionato e che [e-mail sia configurato](/help/communities/email.md). Il valore predefinito è deselezionato.

* **Dimensione file massima**

   Rilevante solo se è selezionato `Allow File Uploads`. Questo campo limita la dimensione (in byte) di un file caricato. Il valore predefinito è 104857600 (10 Mb).

* **Tipi di file consentiti**

   Rilevante solo se è selezionato `Allow File Uploads`. Un elenco separato da virgole di estensioni di file con il separatore &quot;punto&quot;. Ad esempio: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se vengono specificati dei tipi di file, non sarà possibile caricare quelli non specificati. Il valore predefinito non è specificato, pertanto tutti i tipi di file sono consentiti.

* **Max Allega**
dimensione file immaginePertinente solo se l&#39;opzione Consenti caricamenti file è selezionata. Numero massimo di byte di cui può disporre un file immagine caricato. Il valore predefinito è 2097152 (2 Mb).

* **Consenti risposte concatenate**

   Se questa opzione è selezionata, consentire le risposte ai commenti pubblicati sull&#39;argomento. Il valore predefinito è deselezionato.

* **Consenti votazione**

   Se questa opzione è selezionata, includete la funzione di votazione con un argomento. Il valore predefinito è deselezionato.

* **Consenti agli utenti di eliminare commenti e argomenti**

   Se questa opzione è selezionata, consentire ai membri di eliminare i commenti e gli argomenti che hanno pubblicato. Il valore predefinito è deselezionato.

* **Mostra breadcrumb**

   Se questa opzione è selezionata, vengono mostrate le breadcrumb di navigazione nelle pagine dell&#39;argomento. Il valore predefinito è selezionato.

* **Visualizza badge**

   Se questa opzione è attivata, vengono visualizzati i simboli guadagnati e assegnati [con il post di blog di un membro. ](/help/communities/implementing-scoring.md) Il valore predefinito è deselezionato.

* **Consenti membri privilegiati**

   Se questa opzione è selezionata, solo i membri con privilegi possono creare contenuto.

* **Membri privilegiati consentiti**

   Aggiungete i membri privilegiati autorizzati a creare contenuto.

* **Blocca i contenuti generati dagli utenti in modalità di modifica Creazione**

   Se attivato, blocca il contenuto generato dall&#39;utente durante la modifica in modalità Autore.

* **Abilita menzione**

   Se abilitata, consente agli utenti della community registrati di identificare altri membri registrati (utilizzando nome, cognome, nome utente) e di assegnare loro un tag utilizzando la sintassi comune @user-name. Gli utenti con tag ricevono notifiche sulle proprie menzioni.

* **Max menzioni**

   Limita il numero massimo di menzioni consentite in un post. Il valore predefinito è 10.

* **Pattern menzioni interfaccia**

   Specificare la stringa di pattern consentita per assegnare un tag (@reference) all&#39;utente registrato in un post. Esempio `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Potrebbe essere necessario controllare sia `AllowThreaded Replies` che `Allow users to Delete Comments and Topics` per abilitare i commenti su un argomento.

#### Scheda Moderazione utente {#user-moderation-tab}

Nella scheda **Moderazione utente**, specificare la modalità di gestione degli argomenti e delle risposte inviati (contenuto generato dall&#39;utente). Per ulteriori informazioni, vedere [Moderazione dei contenuti generati dall&#39;utente](/help/communities/moderate-ugc.md).

* **Rifiuta post**

   Se questa opzione è attivata, i moderatori di membri attendibili potranno negare i post e impedirne la visualizzazione nel forum pubblico. Il valore predefinito è deselezionato.

* **Chiudi/Riapri argomenti**

   Se questa opzione è attivata, i moderatori di membri attendibili potrebbero chiudere un argomento per ulteriori modifiche e commenti e riaprire un argomento. Il valore predefinito è deselezionato.

* **Sposta argomenti**

   Se questa opzione è selezionata, consentite ai moderatori lato pubblicazione di spostare gli argomenti. Il valore predefinito è selezionato.

* **Segnala post**

   Se questa opzione è selezionata, consentire ai membri di contrassegnare gli argomenti o i commenti di altri utenti in modo inappropriato. Il valore predefinito è deselezionato.

* **Elenco di motivi per segnalazione**

   Se questa opzione è selezionata, consentire ai membri di scegliere, da un elenco a discesa, il motivo per cui segnalano un argomento o un commento come inappropriato. Il valore predefinito è deselezionato.

* **Motivo per segnalazione personalizzato**

   Se questa opzione è selezionata, consentire ai membri di inserire il proprio motivo per cui un argomento o un commento viene contrassegnato come inappropriato. Il valore predefinito è deselezionato.

* **Soglia moderazione**

   Immettere il numero di volte in cui un argomento o un commento deve essere contrassegnato dai membri prima che i moderatori ricevano una notifica. Il valore predefinito è 1 (una volta).

* **Limite segnalazione**

   Immettete il numero di volte in cui un argomento o un commento deve essere contrassegnato prima che venga nascosto dalla visualizzazione pubblica. Se è impostato su -1, l&#39;argomento o il commento contrassegnato non viene mai nascosto dalla visualizzazione pubblica. In caso contrario, questo numero deve essere maggiore o uguale alla soglia di moderazione. Il valore predefinito è 5.

#### Scheda Campo tag {#tag-field-tab}

Nella scheda **Tag field** (Campo tag), i tag che possono essere applicati, se consentiti nella scheda **Settings** (Impostazioni), sono limitati in base agli spazi dei nomi scelti.

* **Namespace consentiti**

   Pertinente se `Allow Tagging` è selezionato nella scheda **Settings**. I tag che possono essere applicati sono limitati a quelli all&#39;interno delle categorie dello spazio nomi selezionate. L’elenco degli spazi dei nomi include &quot;Tag standard&quot; (lo spazio dei nomi predefinito) e &quot;Includi tutti i tag&quot;. Il valore predefinito non è selezionato, il che significa che tutti gli spazi dei nomi sono consentiti.

* **Limite di suggerimenti**

   Immettete il numero di tag da visualizzare come suggerimento al membro che invia il messaggio al forum. Il valore predefinito è **-**1 (nessun limite).

#### Scheda Traduzione {#translation-tab}

Nella scheda **Translation**, se la traduzione è abilitata per il sito della community, è possibile impostare la traduzione per tradurre l&#39;intero argomento o i post selezionati.

* **Traduci tutto**

   Se questa opzione è attivata, il thread del forum viene tradotto nella lingua preferita dell&#39;utente. Il valore predefinito è deselezionato.

#### Scheda Ordina impostazioni {#sort-settings-tab}

Nella scheda **Ordina impostazioni**, specificare in che modo i commenti inviati vengono ordinati quando vengono visualizzati.

* **Ordina per**

   Selezionare tutte le selezioni di ordinamento consentite: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. Il valore predefinito è `Newest, Oldest, Last Updated`.

* **Imposta come predefinito**

   Estrai per selezionare una delle opzioni di ordinamento selezionate da visualizzare come predefinita. Il valore predefinito è `Newest`.

* **Seleziona le opzioni di tempo per l&#39;ordinamento Analytics**

   Per selezionare una delle opzioni seguenti, effettuate il pull down: `All, Last 24 Hours, Last 7 Days, Last 30 Days`.

   Il valore predefinito è `All`.

### Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Forum Essentials](/help/communities/essentials-forum.md) per gli sviluppatori.

Per la moderazione degli argomenti e dei commenti pubblicati, vedere [Moderazione dei contenuti generati dall&#39;utente](/help/communities/moderate-ugc.md).

Per assegnare tag agli argomenti e ai commenti inviati, consultate [Assegnazione di tag ai contenuti generati dall&#39;utente](/help/communities/tag-ugc.md).

Per la traduzione di argomenti e commenti pubblicati, vedere [Traduzione di contenuti generati dall&#39;utente](/help/communities/translate-ugc.md).
