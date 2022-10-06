---
title: Funzione Libreria file
seo-title: File Library Feature
description: La funzione Libreria file consente ai visitatori del sito con accesso di caricare, gestire e scaricare file
seo-description: The File Library feature lets signed-in site visitors upload, manage, and download files
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
exl-id: 05cfaab5-a12d-475f-9095-a9fb13571d0a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 9%

---

# Funzione Libreria file{#file-library-feature}

## Introduzione {#introduction}

La funzione di libreria dei file consente ai visitatori del sito che hanno effettuato l’accesso (membri della community) di caricare, gestire e scaricare file all’interno del sito della community.

Questa sezione della documentazione descrive:

* Aggiunta della funzionalità di libreria file a un sito AEM.
* Impostazioni di configurazione per `File Library` componente.

### Aggiunta di una libreria di file a una pagina {#adding-a-file-library-to-a-page}

Per aggiungere una `File Library` in una pagina in modalità di authoring, individua il componente:

* `Communities / File Library`

e trascinarlo nella posizione desiderata su una pagina.

Per le informazioni necessarie, visita [Nozioni di base sui componenti di Communities](/help/communities/basics.md).

Quando il [librerie lato client richieste](/help/communities/essentials-file-library.md#essentials-for-client-side) sono inclusi, è così che `File Library` apparirà il componente:

![file-library1](assets/file-library1.png)

### Configurazione della libreria dei file {#configuring-file-library}

Seleziona il `File Library` per accedere e selezionare il `Configure` che apre la finestra di dialogo di modifica.

![configure-new](assets/configure-new.png)

![file-library2](assets/file-library2.png)

#### Scheda Commenti {#comments-tab}

Sotto la **Commenti** scheda , specifica se e come vengono visualizzati i commenti per i file caricati:

* **Consenti commenti sui file**

   Se questa opzione è selezionata, consenti commenti sui file caricati. Il valore predefinito è deselezionato.

* **Commenti per pagina**

   Limita il numero di commenti visualizzati per pagina e il numero di risposte visualizzate. Il valore predefinito è **10**.

* **Dimensione file massima**

   Questo valore limiterà la dimensione del file caricato. Il limite predefinito è 104857600 (10 Mb).

* **Lunghezza massima messaggio**

   Numero massimo di caratteri che possono essere immessi nella casella di testo. Il valore predefinito è 4096 caratteri.

* **Tipi di file consentiti**

   Elenco di estensioni di file separate da virgola con il separatore &quot;punto&quot;. Ad esempio: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se sono specificati tipi di file, quelli non specificati non saranno consentiti. Il valore predefinito non è specificato in modo che tutti i tipi di file siano consentiti.

* **Editor Rich Text**

   Se questa opzione è selezionata, è possibile inserire commenti con markup. Il valore predefinito è deselezionato.

* **Elimina commenti**

   Se questa opzione è selezionata, gli utenti possono eliminare i propri commenti. Il valore predefinito è selezionato.

* **Consenti assegnazione tag**

   Se questa opzione è selezionata, verrà abilitata la possibilità di aggiungere un tag al file . Il valore predefinito è deselezionato.

* **Namespace consentiti**

   Se l’opzione Consenti assegnazione tag è selezionata, i tag disponibili saranno limitati ai namespace selezionati. Se non ne è selezionata alcuna, sono consentiti tutti. Il valore predefinito è tutti i namespace.

* **Limite di suggerimenti**

   Se l’opzione Consenti assegnazione tag è selezionata, il numero di tag suggeriti da visualizzare è limitato. Se è impostato su -1, non vi è alcun limite. Il valore predefinito è -1.

* **Consenti votazione**

   Se questa opzione è selezionata, verrà abilitata la possibilità di votare un file. Il valore predefinito è deselezionato.

* **Consenti Segui**

   Se questa opzione è selezionata, includi la seguente funzione per gli articoli di blog, che consente ai membri di essere [notificato](/help/communities/notifications.md) di nuovi posti. Il valore predefinito è deselezionato.

* **Abilita menzione**

   Se attivato, consente agli utenti della community registrata di identificare altri membri registrati (utilizzando nome, cognome, nome utente) e di assegnare loro un tag utilizzando la comune sintassi @user-name. Gli utenti con tag ricevono notifiche sulle loro menzioni.

* **Max menzioni**

   Limita il numero massimo di menzioni consentite in un post. Il valore predefinito è 10.

* **Pattern menzioni interfaccia**

   Specifica la stringa di pattern consentita per assegnare il tag (@menzione) all’utente registrato in un post. Esempio ~{{familyName}}{{givenName}}.

* **Consenti risposte concatenate**

   Se questa opzione è selezionata, consenti risposte ai commenti inviati. Il valore predefinito è deselezionato.

#### Scheda Moderazione utente {#user-moderation-tab}

Sotto la **Moderazione utente** , configura la moderazione dei commenti, se i commenti sono consentiti :

* **Premoderazione**

   Se questa opzione è selezionata, i commenti devono essere approvati prima che vengano visualizzati su un sito di pubblicazione. Il valore predefinito è deselezionato.

* **Elimina commenti**

   Se questa opzione è selezionata, il visitatore che ha pubblicato il commento potrà eliminarlo. Il valore predefinito è selezionato.

* **Rifiuta commenti**

   Se questa opzione è selezionata, consentire ai moderatori membri attendibili di negare i commenti. Il valore predefinito è deselezionato.

* **Chiudi/Riapri commenti**

   Se questa opzione è selezionata, consentire ai moderatori membri attendibili di chiudere e riaprire i commenti. Il valore predefinito è deselezionato.

* **Segnala commenti**

   Se questa opzione è selezionata, consenti ai visitatori di contrassegnare i commenti come inappropriati. Il valore predefinito è deselezionato.

* **Elenco di motivi per segnalazione**

   Se questa opzione è selezionata, consenti ai visitatori di scegliere, da un elenco a discesa, il motivo per cui contrassegnano un commento come inappropriato. Il valore predefinito è deselezionato.

* **Motivo per segnalazione personalizzato**

   Se questa opzione è selezionata, consenti ai visitatori di inserire il proprio motivo per contrassegnare un commento come inappropriato. Il valore predefinito è deselezionato.

* **Soglia moderazione**

   Immetti il numero di volte in cui un commento deve essere segnalato dai visitatori prima che i moderatori vengano informati. Il valore predefinito è una tantum (**1**).

* **Limite segnalazione**

   Immetti il numero di volte in cui un commento deve essere contrassegnato prima che venga nascosto dalla visualizzazione pubblica. Questo numero deve essere maggiore o uguale a **Soglia moderazione**. Il valore predefinito è 5.

### Scheda Impostazioni di ordinamento {#sort-settings-tab}

Ordina per

Imposta come predefinito

### Informazioni aggiuntive {#additional-information}

Per ulteriori informazioni, consulta [Nozioni di base sulla libreria dei file](/help/communities/essentials-file-library.md) per sviluppatori.

Per la moderazione degli argomenti e dei commenti pubblicati, vedi [Moderazione dei contenuti generati dagli utenti](/help/communities/moderate-ugc.md).

Per assegnare tag agli argomenti e ai commenti pubblicati, vedi [Assegnazione tag ai contenuti generati dagli utenti](/help/communities/tag-ugc.md).
