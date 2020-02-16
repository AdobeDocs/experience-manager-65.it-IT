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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Funzione Libreria file{#file-library-feature}

## Introduzione {#introduction}

La funzione di libreria dei file consente ai visitatori del sito che hanno effettuato l&#39;accesso (membri della community) di caricare, gestire e scaricare i file all&#39;interno del sito della community.

Questa sezione della documentazione descrive

* aggiunta della funzione di libreria file a un sito AEM
* impostazioni di configurazione per il `File Library` componente

### Aggiunta di una libreria di file a una pagina {#adding-a-file-library-to-a-page}

Per aggiungere un `File Library` componente a una pagina in modalità di creazione, individuare il componente

* `Communities / File Library`

e trascinarlo nella posizione desiderata su una pagina.

Per le informazioni necessarie, visita [Community Components Basics](/help/communities/basics.md).

Quando sono incluse le librerie [lato client](/help/communities/essentials-file-library.md#essentials-for-client-side) richieste, verrà visualizzato il `File Library` componente:

![chlimage_1-145](assets/chlimage_1-145.png)

### Configurazione della libreria dei file {#configuring-file-library}

Selezionate il `File Library` componente inserito a cui accedere e selezionate l’ `Configure` icona che apre la finestra di dialogo di modifica.

![chlimage_1-146](assets/chlimage_1-146.png) ![forum-config-1](assets/forum-config-1.png)

#### Scheda Commenti {#comments-tab}

Nella scheda **Commenti **specificare se e come vengono visualizzati i commenti per i file caricati:

* **Consenti commenti sui file** Se questa opzione è selezionata, consenti commenti sui file caricati. Il valore predefinito è deselezionato.

* **Commenti per pagina** Limita il numero di commenti visualizzati per pagina e il numero di risposte visualizzate. Default is **10**.

* **Dimensione** massima file Questo valore limita le dimensioni del file caricato. Il limite predefinito è 104857600 (10 Mb).

* **Lunghezza** massima messaggio Numero massimo di caratteri che possono essere immessi nella casella di testo. Il valore predefinito è 4096 caratteri.

* **Tipi** di file consentiti Elenco separato da virgole di estensioni di file con il separatore &quot;punto&quot;. Ad esempio: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se vengono specificati dei tipi di file, quelli non specificati non saranno consentiti. Il valore predefinito non è specificato in modo che** **tutti i tipi di file siano consentiti.

* **Editor** Rich Text Se questa opzione è selezionata, è possibile inserire commenti con tag. Il valore predefinito è deselezionato.

* **Elimina commenti** Se questa opzione è selezionata, gli utenti possono eliminare i propri commenti. Il valore predefinito è selezionato.

* **Consenti tag** Se questa opzione è selezionata, verrà abilitata la possibilità di aggiungere al file un tag. Il valore predefinito è deselezionato.

* **Spazi dei nomi consentiti** Se l’opzione Consenti tag è selezionata, i tag disponibili saranno limitati agli spazi dei nomi selezionati. Se non ne è selezionata alcuna, sono tutti consentiti. Il valore predefinito è tutti gli spazi dei nomi.

* **Limite** suggerimenti Se l’opzione Consenti tag è selezionata, questa impostazione limita il numero di tag suggeriti da visualizzare. Se è impostato su -1, non è previsto alcun limite. Il valore predefinito è -1.

* **Consenti votazione** Se questa opzione è selezionata, la possibilità di votare per un file verrà abilitata. Il valore predefinito è deselezionato.

* **Consenti** se questa opzione è selezionata, includete la seguente funzione per gli articoli di blog, che consente ai membri di ricevere [notifiche](/help/communities/notifications.md) per i nuovi post. Il valore predefinito è deselezionato.

* **Abilita menzioni** Se abilitata, consente agli utenti della community registrati di identificare altri membri registrati (utilizzando nome, cognome, nome utente) e di assegnare loro un tag utilizzando la sintassi comune @user-name. Gli utenti con tag ricevono notifiche sulle proprie menzioni.

* **N. max menzioni** Limita il numero massimo di menzioni consentite in un post. Il valore predefinito è 10.

* **Pattern** di menzione dell&#39;interfaccia utente Specificate la stringa di pattern consentita per assegnare un tag (@reference) all&#39;utente registrato in un post. Ad esempio ~{{familyName}}{{givenName}}.

* **Consenti risposte** filettate se questa opzione è selezionata, consenti risposte ai commenti inviati. Il valore predefinito è deselezionato.

#### Scheda Moderazione utente {#user-moderation-tab}

Nella scheda Moderazione **** utente configurate la moderazione dei commenti, se i commenti sono consentiti:

* **Pre-moderazione** Se questa opzione è selezionata, i commenti devono essere approvati prima che vengano visualizzati su un sito di pubblicazione. Il valore predefinito è deselezionato.

* **Elimina commenti** Se questa opzione è selezionata, il visitatore che ha pubblicato il commento può eliminarlo. Il valore predefinito è selezionato.

* **Rifiuta commenti** Se questa opzione è selezionata, consente ai moderatori membri attendibili di negare i commenti. Il valore predefinito è deselezionato.

* **Chiudi/Riapri commenti** Se questa opzione è selezionata, consente ai moderatori membri attendibili di chiudere e riaprire i commenti. Il valore predefinito è deselezionato.

* **Contrassegna commenti** Se questa opzione è selezionata, i visitatori possono contrassegnare i commenti come non appropriati. Il valore predefinito è deselezionato.

* **Elenco** motivi contrassegno Se questa opzione è selezionata, i visitatori possono scegliere, da un elenco a discesa, il motivo per cui contrassegnare un commento come non appropriato. Il valore predefinito è deselezionato.

* **Motivo** contrassegno personalizzato Se questa opzione è selezionata, i visitatori possono immettere il proprio motivo per cui un commento viene contrassegnato come inappropriato. Il valore predefinito è deselezionato.

* **Soglia** moderazione Consente di specificare quante volte un commento deve essere contrassegnato dai visitatori prima che i moderatori ricevano una notifica. Il valore predefinito è una tantum (**1**).

* **Limite** contrassegno Consente di specificare quante volte deve essere segnalato un commento prima di essere nascosto nella visualizzazione pubblica. Questo numero deve essere maggiore o uguale alla soglia di **moderazione**. Il valore predefinito è 5.

### Scheda Impostazioni ordinamento {#sort-settings-tab}

Ordina per

Imposta come predefinito

### Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [File Library Essentials](/help/communities/essentials-file-library.md) per gli sviluppatori.

Per la moderazione degli argomenti e dei commenti pubblicati, consultate [Moderazione del contenuto](/help/communities/moderate-ugc.md)generato dall&#39;utente.

Per assegnare tag agli argomenti e ai commenti inviati, consultate [Assegnazione di tag ai contenuti](/help/communities/tag-ugc.md)generati dagli utenti.
