---
title: Funzione Libreria file
description: La funzione Libreria file consente ai visitatori del sito che hanno effettuato l'accesso di caricare, gestire e scaricare file.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 05cfaab5-a12d-475f-9095-a9fb13571d0a
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 1%

---

# Funzione Libreria file{#file-library-feature}

## Introduzione {#introduction}

La funzionalità raccolta file consente ai visitatori del sito (membri della comunità) che hanno effettuato l&#39;accesso di caricare, gestire e scaricare file all&#39;interno del sito della comunità.

Questa sezione della documentazione descrive:

* Aggiunta della funzionalità di libreria file a un sito AEM.
* Impostazioni di configurazione per il componente `File Library`.

### Aggiunta di una libreria di file a una pagina {#adding-a-file-library-to-a-page}

Per aggiungere un componente `File Library` a una pagina in modalità di creazione, individua il componente:

* `Communities / File Library`

Trascinarlo nella posizione desiderata su una pagina.

Per informazioni necessarie, visitare [Nozioni di base sui componenti delle community](/help/communities/basics.md).

Quando sono incluse le [librerie lato client richieste](/help/communities/essentials-file-library.md#essentials-for-client-side), è così che viene visualizzato il componente `File Library`:

![file-library1](assets/file-library1.png)

### Configurazione della libreria dei file {#configuring-file-library}

Selezionare il componente `File Library` inserito in modo da poter accedere e selezionare l&#39;icona `Configure` che apre la finestra di dialogo di modifica.

![configura-nuovo](assets/configure-new.png)

![file-library2](assets/file-library2.png)

#### Scheda Commenti {#comments-tab}

Nella scheda **Commenti**, specifica se e come vengono visualizzati i commenti per i file caricati:

* **Consenti commenti su file**

  Se questa opzione è selezionata, consenti commenti sui file caricati. L&#39;impostazione predefinita è deselezionata.

* **Commenti Per Pagina**

  Limita il numero di commenti visualizzati per pagina e il numero di risposte visualizzate. Il valore predefinito è **10**.

* **Dimensione massima file**

  Questo valore limita la dimensione del file caricato. Il limite predefinito è 104857600 (10 MB).

* **Lunghezza massima messaggio**

  Numero massimo di caratteri che possono essere immessi nella casella di testo. Il valore predefinito è 4096 caratteri.

* **Tipi di file consentiti**

  Un elenco separato da virgole di estensioni di file con il separatore &quot;punto&quot;. Ad esempio, .jpg, .jpeg, .png, .doc, .docx, .pdf. Se sono specificati tipi di file, non sono consentiti i tipi di file non specificati. Il valore predefinito non è specificato in modo che siano consentiti tutti i tipi di file.

* **Editor Rich Text**

  Se questa opzione è selezionata, è possibile immettere commenti con markup. L&#39;impostazione predefinita è deselezionata.

* **Elimina commenti**

  Se questa opzione è selezionata, gli utenti possono eliminare i propri commenti. Il valore predefinito è selezionato.

* **Consenti assegnazione tag**

  Se questa opzione è selezionata, la possibilità di aggiungere un tag al file è abilitata. L&#39;impostazione predefinita è deselezionata.

* **Spazi dei nomi consentiti**

  Se è selezionata l’opzione Consenti assegnazione tag, i tag disponibili sono limitati agli spazi dei nomi selezionati. Se non è selezionato alcuno spazio dei nomi, sono consentiti tutti. Il valore predefinito è tutti gli spazi dei nomi.

* **Limite suggerimenti**

  Se è selezionata l’opzione Consenti assegnazione tag, questa impostazione limita il numero di tag suggeriti da visualizzare. Se è impostato su -1, non esiste alcun limite. Il valore predefinito è -1.

* **Consenti votazione**

  Se questa opzione è selezionata, la possibilità di votare per un file è abilitata. L&#39;impostazione predefinita è deselezionata.

* **Consenti Segui**

  Se questa opzione è selezionata, includere la seguente funzionalità per gli articoli di blog, che consente ai membri di ricevere [notifica](/help/communities/notifications.md) dei nuovi post. L&#39;impostazione predefinita è deselezionata.

* **Abilita menzione**

  Se questa opzione è attivata, consente agli utenti registrati della community di identificare altri membri registrati (tramite nome, cognome, nome utente) e di assegnare loro tag utilizzando la sintassi @user-name comune. Gli utenti taggati ricevono notifiche sulle loro menzioni.

* **Max menzioni**

  Limita il numero massimo di menzioni consentite in un post. Il valore predefinito è 10.

* **Pattern menzioni interfaccia utente**

  Specifica la stringa di pattern consentita in modo da assegnare tag (@mention) all’utente registrato in un post. Esempio: `~{{familyName}}{{givenName}}`.

* **Consenti risposte concatenate**

  Se questa opzione è selezionata, consenti le risposte ai commenti pubblicati. L&#39;impostazione predefinita è deselezionata.

#### Scheda Moderazione utente {#user-moderation-tab}

Nella scheda **Moderazione utente** configura la moderazione dei commenti, se i commenti sono consentiti:

* **Pre-moderazione**

  Se questa opzione è selezionata, i commenti devono essere approvati prima di essere visualizzati in un sito pubblicato. L&#39;impostazione predefinita è deselezionata.

* **Elimina commenti**

  Se questa opzione è selezionata, il visitatore che ha pubblicato il commento può eliminarlo, se lo desidera. Il valore predefinito è selezionato.

* **Rifiuta commenti**

  Se questa opzione è selezionata, consentire ai moderatori membri attendibili di rifiutare i commenti. L&#39;impostazione predefinita è deselezionata.

* **Chiudi/Riapri commenti**

  Se questa opzione è selezionata, consentire ai moderatori membri attendibili di chiudere e riaprire i commenti. L&#39;impostazione predefinita è deselezionata.

* **Contrassegna commenti**

  Se questa opzione è selezionata, consenti ai visitatori di segnalare i commenti non appropriati. L&#39;impostazione predefinita è deselezionata.

* **Elenco motivi contrassegno**

  Se questa opzione è selezionata, consenti ai visitatori di scegliere, da un elenco a discesa, il motivo per cui segnalare un commento come inappropriato. L&#39;impostazione predefinita è deselezionata.

* **Motivo contrassegno personalizzato**

  Se questa opzione è selezionata, consenti ai visitatori di inserire il proprio motivo per segnalare un commento non appropriato. L&#39;impostazione predefinita è deselezionata.

* **Soglia moderazione**

  Immetti il numero di volte in cui un commento deve essere segnalato dai visitatori prima che il moderatore riceva una notifica. Il valore predefinito è una tantum (**1**).

* **Limite di segnalazione**

  Immettere il numero di volte in cui un commento deve essere segnalato prima di essere nascosto alla visualizzazione pubblica. Questo numero deve essere maggiore o uguale alla **soglia di moderazione**. Il valore predefinito è 5.

### Scheda Impostazioni ordinamento {#sort-settings-tab}

Ordina per

Imposta come predefinito

### Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Nozioni di base sulla libreria dei file](/help/communities/essentials-file-library.md) per gli sviluppatori.

Per la moderazione degli argomenti e dei commenti pubblicati, vedere [Moderazione dei contenuti generati dagli utenti](/help/communities/moderate-ugc.md).

Per assegnare tag agli argomenti e ai commenti pubblicati, vedere [Assegnazione di tag ai contenuti generati dagli utenti](/help/communities/tag-ugc.md).
