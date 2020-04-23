---
title: Ideazione
seo-title: Ideazione
description: Aggiunta e configurazione della funzione Ideazione
seo-description: Aggiunta e configurazione della funzione Ideazione
uuid: 38468290-6d00-4ee4-91d8-7c2e8ae32712
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a3f5a21d-2df6-4663-a1ea-3a067c46f860
docset: aem65
translation-type: tm+mt
source-git-commit: 85f3b8f2a5f079954f4907037c1c722a6b25fd91

---


# Ideazione {#ideation-feature}

## Introduzione {#introduction}

La funzione di ideazione fornisce un’area per i visitatori del sito che hanno effettuato l’accesso (membri della community) nell’ambiente di pubblicazione per:

* Create idee da condividere con la community.
* Visualizza e commenta le idee.
* Seguite un&#39;idea.
* Votate su un&#39;idea.

Questa sezione della documentazione descrive quanto segue:

* Aggiunta della funzione di ideazione a un sito AEM.
* Impostazioni di configurazione per il componente Ideazione.

### Adding a Ideation to a Page {#adding-a-ideation-to-a-page}

Per aggiungere un `Ideation` componente a una pagina in modalità di creazione, usate il browser Componenti per individuare

* `Communities / Ideation`

e trascinatela nella posizione desiderata su una pagina in cui deve comparire l’idea.

Per le informazioni necessarie, consulta [Community Components Basics](/help/communities/basics.md).

Quando sono incluse le librerie [lato client](/help/communities/ideation.md#essentials-for-client-side) richieste, verrà visualizzato il `Ideation` componente:

![chlimage_1-71](assets/chlimage_1-71.png)

### Configurazione di un&#39;idea {#configuring-an-ideation}

Selezionate il `Ideation` componente inserito a cui accedere e selezionate l’ `Configure` icona che apre la finestra di dialogo di modifica.

![chlimage_1-72](assets/chlimage_1-72.png) ![ideation-settings](assets/ideation-settings.png)

#### scheda Impostazioni {#settings-tab}

Nella scheda **[!UICONTROL Impostazioni]** , specificate le impostazioni per idee e commenti:

* **Consenti miniatura allegato**
* **Dimensione max miniatura allegato**
* **Dimensioni minime immagine per miniatura**
* **Dimensione massima miniatura**
* **Consenti membri privilegiati**
* **Membri privilegiati consentiti**
* **Blocca i contenuti generati dagli utenti in modalità di modifica Creazione**
* **Titolo ideazione**

* Titolo visualizzato per l’idea. Default is `Ideation`.
* **Descrizione ideazione**

   Descrizione da visualizzare come sottotitolo per l’idea. Il valore predefinito non è una descrizione.

* **Topic per pagina**

   Definisce il numero di idee/post mostrati per pagina. Il valore predefinito è 10.

* **Moderato**

   Se questa opzione è attivata, le idee e i commenti devono essere approvati prima che vengano visualizzati su un sito di pubblicazione. Il valore predefinito è deselezionato.

* **Chiuso**

   Se questa opzione è selezionata, il forum di ideazione è chiuso a nuove idee e commenti. Il valore predefinito è deselezionato.

* **Editor Rich Text**

   Se questa opzione è selezionata, è possibile inserire idee e commenti con la marcatura. Il valore predefinito è deselezionato.

* **Consenti assegnazione tag**

   Se questa opzione è selezionata, consentire ai membri di aggiungere etichette di tag al proprio post (consultate la scheda Campo **** tag ). Il valore predefinito è deselezionato.

* **Consenti caricamenti file**

   Se questa opzione è selezionata, consentite l&#39;aggiunta di allegati all&#39;idea o al commento. Il valore predefinito è deselezionato.

* **Dimensione file massima**

   Pertinente solo se `Allow File Uploads` è controllato. Questo campo limita la dimensione (in byte) di un file caricato. Il valore predefinito è 104857600 (10 Mb).

* **Tipi di file consentiti**

   Pertinente solo se `Allow File Uploads` è controllato. Un elenco separato da virgole di estensioni di file con il separatore &quot;punto&quot;. Ad esempio: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se vengono specificati dei tipi di file, non sarà possibile caricare quelli non specificati. Il valore predefinito non è specificato, pertanto tutti i tipi di file sono consentiti.

* **Dimensione massima per file immagine allegato**

   Pertinente solo se l&#39;opzione Consenti caricamenti file è selezionata. Numero massimo di byte di cui può disporre un file immagine caricato. Il valore predefinito è 2097152 (2 Mb).

* **Consenti risposte**

   Se questa opzione è attivata, consenti le risposte ai commenti pubblicati sull&#39;idea. Il valore predefinito è deselezionato.

* **Consenti votazione**

   Se questa opzione è selezionata, consentire la votazione dei commenti di un&#39;idea. Il valore predefinito è deselezionato.

* **Consenti agli utenti di eliminare commenti e argomenti**

   Se questa opzione è selezionata, consentire ai membri di eliminare i commenti e le idee che hanno pubblicato. Il valore predefinito è deselezionato.

* **Consenti Segui**

   Se questa opzione è selezionata, includete la seguente funzione per i post di idee, che consente ai membri di ricevere [notifiche](/help/communities/notifications.md) sui nuovi post. Il valore predefinito è deselezionato.

* **Consenti iscrizioni e-mail**

   Se questa opzione è attivata, consentite ai membri di ricevere notifiche relative ai nuovi post via e-mail ([iscrizione](/help/communities/subscriptions.md)). Richiede `Allow Following` di essere selezionato e configurato [per l’](/help/communities/email.md)e-mail. Il valore predefinito è deselezionato.

* **Consenti votazione**

   Se questa opzione è selezionata, consentire la votazione dei commenti di un&#39;idea. Il valore predefinito è deselezionato.

* **Visualizza badge**

   Se questa opzione è selezionata, vengono visualizzati [i simboli](/help/communities/implementing-scoring.md) guadagnati e assegnati con l&#39;idea di un membro. Il valore predefinito è deselezionato.

* **Non ricevere risposte sulla pagina di elenco**

* **Consenti contenuto in primo piano**

   Se questa opzione è selezionata, l’idea può essere identificata come contenuto [](/help/communities/featured.md)disponibile. Il valore predefinito è deselezionato.

* **Abilita menzione**
* **Max menzioni**
* **Pattern menzioni interfaccia**

#### Scheda Moderazione utente {#user-moderation-tab}

Nella scheda Moderazione **** utente, specificate le modalità di gestione delle idee e dei commenti pubblicati (contenuto generato dall’utente). Per ulteriori informazioni, consultate [Moderazione del contenuto](/help/communities/moderate-ugc.md)generato dall&#39;utente.

* **Rifiuta post**

   Se questa opzione è attivata, i moderatori di membri attendibili potranno negare i post e impedirne la visualizzazione nel forum pubblico. Il valore predefinito è deselezionato.

* **Chiudi/Riapri argomenti**

   Se questa opzione è attivata, i moderatori di membri attendibili potrebbero chiudere un argomento per ulteriori modifiche e commenti e riaprire un argomento. Il valore predefinito è deselezionato.

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

Nella scheda Campo **** tag, i tag che possono essere applicati, se consentiti nella scheda **[!UICONTROL Impostazioni]** , sono limitati in base agli spazi dei nomi selezionati.

* **Namespace consentiti**

   Pertinente se `Allow Tagging` è selezionato sotto la scheda **[!UICONTROL Impostazioni]** . I tag che possono essere applicati sono limitati a quelli all&#39;interno delle categorie dello spazio nomi selezionate. L&#39;elenco degli spazi dei nomi include &quot;Tag standard&quot; (lo spazio dei nomi predefinito) e &quot;Includi tutti i tag&quot;. Il valore predefinito non è selezionato, il che significa che tutti gli spazi dei nomi sono consentiti.

* **Limite di suggerimenti**

   Immettete il numero di tag da visualizzare come suggerimento al membro che invia il messaggio al forum. Un valore pari a **-1** non indica alcun limite. Il valore predefinito è 0.

#### Scheda Impostazioni ordinamento {#sort-settings-tab}

Nella scheda **[!UICONTROL Impostazioni]** ordinamento, specificare in che modo i commenti inviati vengono ordinati quando vengono visualizzati.

* **Ordina per**

   Seleziona tutte le selezioni di ordinamento consentite: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. Default is `Newest, Oldest, Last Updated`.

* **Imposta come predefinito**

   Estrai per selezionare una delle opzioni di ordinamento selezionate da visualizzare come predefinita. Default is `Newest`.

* **Seleziona le opzioni di tempo per l&#39;ordinamento Analytics**

   Per selezionare una delle due opzioni, trascinate verso il basso `All, Last 24 Hours, Last 7 Days, Last 30 Days`. Default is `All`.

## Esperienza dei visitatori del sito {#site-visitor-experience}

### Creazione di Idea {#creating-idea}

Come per tutte le funzioni Community, se non è stato effettuato l’accesso, un visitatore del sito può solo leggere idee e visualizzare altre opinioni (tramite commenti e voti/clic).

Una volta effettuato l’accesso, un membro può creare una nuova idea.

![chlimage_1-73](assets/chlimage_1-73.png)

Prima di inviare l&#39;idea, è possibile salvare una bozza.

Selezionando il `Save as Draft` pulsante, viene salvata una bozza.

![chlimage_1-74](assets/chlimage_1-74.png)

Quando visualizzate le bozze salvate nella `My Drafts` scheda, selezionate `Read More` di nuovo la modalità di modifica:

![chlimage_1-75](assets/chlimage_1-75.png)

#### Feedback {#providing-feedback}

Una volta pubblicata l&#39;idea, altri membri possono accedere, aprire l&#39;idea ( `Read More`) e come l&#39;idea, aggiungendo così al conteggio dei voti, e fare commenti.

![chlimage_1-76](assets/chlimage_1-76.png)

### Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Ideation Essentials](/help/communities/ideation.md) per gli sviluppatori.

Per la moderazione degli argomenti e dei commenti pubblicati, consultate [Moderazione del contenuto](/help/communities/moderate-ugc.md)generato dall&#39;utente.

Per assegnare tag agli argomenti e ai commenti inviati, consultate [Assegnazione di tag ai contenuti](/help/communities/tag-ugc.md)generati dagli utenti.
