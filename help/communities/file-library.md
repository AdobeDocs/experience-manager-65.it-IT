---
title: Funzione Libreria file
seo-title: Funzione Libreria file
description: La funzione Libreria file consente ai visitatori del sito che hanno effettuato l’accesso di caricare, gestire e scaricare i file
seo-description: La funzione Libreria file consente ai visitatori del sito che hanno effettuato l’accesso di caricare, gestire e scaricare i file
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
translation-type: tm+mt
source-git-commit: 9e941ce092f7d3248c11886d6bf1e54f2e726362
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 9%

---


# Funzione Libreria file{#file-library-feature}

## Introduzione {#introduction}

La funzione di libreria dei file consente ai visitatori del sito che hanno effettuato l&#39;accesso (membri della community) di caricare, gestire e scaricare i file all&#39;interno del sito della community.

Questa sezione della documentazione descrive quanto segue:

* Aggiunta della funzione di libreria file a un sito AEM.
* Impostazioni di configurazione per il componente `File Library`.

### Aggiunta di una libreria di file a una pagina {#adding-a-file-library-to-a-page}

Per aggiungere un componente `File Library` a una pagina in modalità di creazione, individuare il componente:

* `Communities / File Library`

e trascinarlo nella posizione desiderata su una pagina.

Per le informazioni necessarie, visitare [Community Components Basics](/help/communities/basics.md).

Quando vengono incluse le [librerie lato client ](/help/communities/essentials-file-library.md#essentials-for-client-side), viene visualizzato il componente `File Library`:

![chlimage_1-430](assets/chlimage_1-430.png)

### Configurazione della libreria di file {#configuring-file-library}

Selezionare il componente `File Library` inserito a cui accedere e selezionare l&#39;icona `Configure` che apre la finestra di dialogo di modifica.

![chlimage_1-431](assets/chlimage_1-431.png)

![chlimage_1-432](assets/chlimage_1-432.png)

#### Scheda Commenti {#comments-tab}

Nella scheda **Commenti**, specificate se e come vengono visualizzati i commenti per i file caricati:

* **Consenti commenti sui file**

   Se questa opzione è selezionata, consentite commenti sui file caricati. Il valore predefinito è deselezionato.

* **Commenti per pagina**

   Limita il numero di commenti visualizzati per pagina e il numero di risposte visualizzate. Il valore predefinito è **10**.

* **Dimensione file massima**

   Questo valore limita le dimensioni del file caricato. Il limite predefinito è 104857600 (10 Mb).

* **Lunghezza massima messaggio**

   Numero massimo di caratteri che possono essere immessi nella casella di testo. Il valore predefinito è 4096 caratteri.

* **Tipi di file consentiti**

   Un elenco separato da virgole di estensioni di file con il separatore &quot;punto&quot;. Ad esempio: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se vengono specificati dei tipi di file, quelli non specificati non saranno consentiti. Il valore predefinito non è specificato in modo che tutti i tipi di file siano consentiti.

* **Editor Rich Text**

   Se questa opzione è selezionata, è possibile inserire commenti con tag. Il valore predefinito è deselezionato.

* **Elimina commenti**

   Se questa opzione è selezionata, gli utenti possono eliminare i propri commenti. Il valore predefinito è selezionato.

* **Consenti assegnazione tag**

   Se questa opzione è selezionata, verrà abilitata la possibilità di aggiungere un tag al file. Il valore predefinito è deselezionato.

* **Namespace consentiti**

   Se l’opzione Consenti tag è selezionata, i tag disponibili saranno limitati agli spazi dei nomi selezionati. Se non ne è selezionata alcuna, sono tutti consentiti. Il valore predefinito è tutti gli spazi dei nomi.

* **Limite di suggerimenti**

   Se l’opzione Consenti tag è selezionata, questa impostazione limita il numero di tag suggeriti da visualizzare. Se è impostato su -1, non è previsto alcun limite. Il valore predefinito è -1.

* **Consenti votazione**

   Se questa opzione è selezionata, verrà abilitata la possibilità di votare un file. Il valore predefinito è deselezionato.

* **Consenti Segui**

   Se questa opzione è attivata, includete la seguente funzione per gli articoli di blog, che consente ai membri di ricevere [notifiche](/help/communities/notifications.md) di nuovi post. Il valore predefinito è deselezionato.

* **Abilita menzione**

   Se abilitata, consente agli utenti della community registrati di identificare altri membri registrati (utilizzando nome, cognome, nome utente) e di assegnare loro un tag utilizzando la sintassi comune @user-name. Gli utenti con tag ricevono notifiche sulle proprie menzioni.

* **Max menzioni**

   Limita il numero massimo di menzioni consentite in un post. Il valore predefinito è 10.

* **Pattern menzioni interfaccia**

   Specificare la stringa di pattern consentita per assegnare un tag (@reference) all&#39;utente registrato in un post. Ad esempio ~{{familyName}}{{givenName}}.

* **Consenti risposte concatenate**

   Se questa opzione è selezionata, consentire le risposte ai commenti inviati. Il valore predefinito è deselezionato.

#### Scheda Moderazione utente {#user-moderation-tab}

Nella scheda **Moderazione utente**, configurare la moderazione dei commenti, se i commenti sono consentiti:

* **Premoderazione**

   Se questa opzione è attivata, i commenti devono essere approvati prima che vengano visualizzati su un sito di pubblicazione. Il valore predefinito è deselezionato.

* **Elimina commenti**

   Se questa opzione è attivata, al visitatore che ha pubblicato il commento viene fornita la possibilità di eliminarlo. Il valore predefinito è selezionato.

* **Rifiuta commenti**

   Se questa opzione è selezionata, consentire ai moderatori membri attendibili di negare i commenti. Il valore predefinito è deselezionato.

* **Chiudi/Riapri commenti**

   Se questa opzione è selezionata, consentire ai moderatori membri attendibili di chiudere e riaprire i commenti. Il valore predefinito è deselezionato.

* **Segnala commenti**

   Se questa opzione è selezionata, consentire ai visitatori di contrassegnare i commenti come non appropriati. Il valore predefinito è deselezionato.

* **Elenco di motivi per segnalazione**

   Se questa opzione è selezionata, consentire ai visitatori di scegliere, da un elenco a discesa, il motivo per cui contrassegnare un commento come non appropriato. Il valore predefinito è deselezionato.

* **Motivo per segnalazione personalizzato**

   Se questa opzione è selezionata, consentite ai visitatori di inserire il proprio motivo per cui un commento viene contrassegnato come inappropriato. Il valore predefinito è deselezionato.

* **Soglia moderazione**

   Immettete il numero di volte in cui un commento deve essere contrassegnato dai visitatori prima che i moderatori ricevano una notifica. Il valore predefinito è una tantum (**1**).

* **Limite segnalazione**

   Specificate quante volte un commento deve essere contrassegnato prima che venga nascosto dalla visualizzazione pubblica. Questo numero deve essere maggiore o uguale alla **Soglia moderazione**. Il valore predefinito è 5.

### Scheda Ordina impostazioni {#sort-settings-tab}

Ordina per

Imposta come predefinito

### Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [File Library Essentials](/help/communities/essentials-file-library.md) per gli sviluppatori.

Per la moderazione degli argomenti e dei commenti pubblicati, vedere [Moderazione dei contenuti generati dall&#39;utente](/help/communities/moderate-ugc.md).

Per assegnare tag agli argomenti e ai commenti inviati, consultate [Assegnazione di tag ai contenuti generati dall&#39;utente](/help/communities/tag-ugc.md).
