---
title: Funzione ideazione
description: Scopri come aggiungere e configurare la funzione di ideazione che consente ai membri della community di creare, visualizzare, seguire, votare e commentare le idee condivise con la community.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: e130bab4-524d-4413-ba8b-53d0ed9e8623
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 10%

---

# Funzione ideazione {#ideation-feature}

## Introduzione {#introduction}

La funzione di ideazione fornisce un’area per i visitatori del sito connessi (membri della community) nell’ambiente di pubblicazione per:

* Creare idee da condividere con la community.
* Visualizzare e commentare le idee.
* Segui un&#39;idea.
* Votate un&#39;idea.

Questa sezione della documentazione descrive:

* Aggiunta della funzione di ideazione a un sito AEM.
* Impostazioni di configurazione del componente Ideazione.

### Aggiunta di un’idea a una pagina {#adding-a-ideation-to-a-page}

Per aggiungere una `Ideation` a una pagina in modalità di authoring, utilizza il browser Componenti per individuare

* `Communities / Ideation`

Trascinarlo nella posizione desiderata su una pagina in cui dovrebbe essere visualizzata l&#39;idea.

Per informazioni necessarie, visitare il sito [Nozioni di base sui componenti community](/help/communities/basics.md).

Quando [librerie lato client richieste](/help/communities/ideation.md#essentials-for-client-side) sono inclusi, è così che `Ideation` viene visualizzato il componente:

![ideazione](assets/ideation.png)

### Configurazione di un’idea {#configuring-an-ideation}

Seleziona la inserita `Ideation` in modo da poter accedere e selezionare `Configure` che apre la finestra di dialogo per modifica.

![configure-new](assets/configure-new.png)

![ideation-settings](assets/ideation-settings.png)

#### Scheda Impostazioni {#settings-tab}

Sotto **[!UICONTROL Impostazioni]** , specificare le impostazioni per idee e commenti:

* **Consenti miniatura allegato**
* **Dimensione max miniatura allegato**
* **Dimensioni minime immagine per miniatura**
* **Dimensione massima miniatura**
* **Consenti membri privilegiati**
* **Membri privilegiati consentiti**
* **Blocca i contenuti generati dagli utenti in modalità di modifica Creazione**
* **Titolo ideazione**

* Titolo visualizzato dell&#39;idea. Il valore predefinito è `Ideation`.
* **Descrizione ideazione**

  Descrizione da visualizzare come sottotitolo dell&#39;idea. Il valore predefinito non è una descrizione.

* **Topic per pagina**

  Definisce il numero di idee/post mostrati per pagina. Il valore predefinito è 10.

* **Moderato**

  Se questa opzione è selezionata, è necessario approvare la pubblicazione di idee e commenti prima di visualizzarli in un sito pubblicato. L&#39;impostazione predefinita è deselezionata.

* **Chiuso**

  Se questa opzione è selezionata, il forum di ideazione è chiuso a nuove idee e commenti. L&#39;impostazione predefinita è deselezionata.

* **Editor Rich Text**

  Se questa opzione è selezionata, è possibile immettere idee e commenti con il markup. L&#39;impostazione predefinita è deselezionata.

* **Consenti assegnazione tag**

  Se questa opzione è selezionata, consentire ai membri di aggiungere etichette tag ai propri post (vedere **[!UICONTROL Campo tag]** ). L&#39;impostazione predefinita è deselezionata.

* **Consenti caricamenti file**

  Se questa opzione è selezionata, consenti l&#39;aggiunta di file allegati all&#39;idea o al commento. L&#39;impostazione predefinita è deselezionata.

* **Dimensione file massima**

  Rilevante solo se `Allow File Uploads` è selezionato. Questo campo limita la dimensione (in byte) di un file caricato. Il valore predefinito è 104857600 (10 Mb).

* **Tipi di file consentiti**

  Rilevante solo se `Allow File Uploads` è selezionato. Un elenco separato da virgole di estensioni di file con il separatore &quot;punto&quot;. Ad esempio, .jpg, .jpeg, .png, .doc, .docx, .pdf. Se sono specificati dei tipi di file, non è possibile caricare quelli non specificati. Il valore predefinito è none specificato, pertanto tutti i tipi di file sono consentiti.

* **Dimensione massima per file immagine allegato**

  Rilevante solo se è selezionata l’opzione Consenti caricamenti file. Numero massimo di byte consentito per un file di immagine caricato. Il valore predefinito è 2097152 (2 Mb).

* **Consenti risposte**

  Se questa opzione è selezionata, consenti le risposte ai commenti inviati all&#39;idea. L&#39;impostazione predefinita è deselezionata.

* **Consenti votazione**

  Se questa opzione è selezionata, consentire la votazione dei commenti di un&#39;idea. L&#39;impostazione predefinita è deselezionata.

* **Consenti agli utenti di eliminare commenti e argomenti**

  Se questa opzione è selezionata, consentire ai membri di eliminare i commenti e le idee pubblicati. L&#39;impostazione predefinita è deselezionata.

* **Consenti Segui**

  Se questa opzione è selezionata, includere la seguente funzionalità per i post di idea, che consente ai membri di essere [notificato](/help/communities/notifications.md) di nuovi posti. L&#39;impostazione predefinita è deselezionata.

* **Consenti iscrizioni e-mail**

  Se questa opzione è selezionata, consenti ai membri di ricevere notifiche sui nuovi post tramite e-mail ([abbonamento](/help/communities/subscriptions.md)). Richiede `Allow Following` da controllare e [e-mail configurato](/help/communities/email.md). L&#39;impostazione predefinita è deselezionata.

* **Consenti votazione**

  Se questa opzione è selezionata, consentire la votazione dei commenti di un&#39;idea. L&#39;impostazione predefinita è deselezionata.

* **Visualizza badge**

  Se questa opzione è selezionata, vengono visualizzati i risultati ottenuti e assegnati [badge](/help/communities/implementing-scoring.md) con l&#39;idea di un membro. L&#39;impostazione predefinita è deselezionata.

* **Non ricevere risposte nella pagina di elenco**

* **Consenti contenuto in primo piano**

  Se questa opzione è selezionata, l’idea è identificabile come [contenuto in primo piano](/help/communities/featured.md). L&#39;impostazione predefinita è deselezionata.

* **Abilita menzione**
* **Max menzioni**
* **Pattern menzioni interfaccia**

#### Scheda Moderazione utente {#user-moderation-tab}

Sotto **[!UICONTROL Moderazione utenti]** , specificare la modalità di gestione delle idee e dei commenti pubblicati (contenuti generati dall&#39;utente). Per ulteriori informazioni, consulta [Moderazione dei contenuti generati dagli utenti](/help/communities/moderate-ugc.md).

* **Rifiuta post**

  Se questa opzione è selezionata, i moderatori membri di fiducia possono negare i post e impedirne la visualizzazione nel forum pubblico. L&#39;impostazione predefinita è deselezionata.

* **Chiudi/Riapri argomenti**

  Se questa opzione è selezionata, i moderatori membri attendibili possono chiudere un argomento per ulteriori modifiche e commenti e riaprire un argomento. L&#39;impostazione predefinita è deselezionata.

* **Segnala post**

  Se questa opzione è selezionata, consentire ai membri di contrassegnare gli argomenti o i commenti di altri utenti come non appropriati. L&#39;impostazione predefinita è deselezionata.

* **Elenco di motivi per segnalazione**

  Se questa opzione è selezionata, consentire ai membri di scegliere, da un elenco a discesa, il motivo per cui contrassegnare un argomento o un commento come non appropriato. L&#39;impostazione predefinita è deselezionata.

* **Motivo per segnalazione personalizzato**

  Se questa opzione è selezionata, consentire ai membri di immettere un motivo specifico per contrassegnare un argomento o un commento come non appropriato. L&#39;impostazione predefinita è deselezionata.

* **Soglia moderazione**

  Immettere il numero di volte in cui un argomento o un commento deve essere segnalato dai membri prima che il moderatore riceva una notifica. Il valore predefinito è 1 (una tantum).

* **Limite segnalazione**

  Immettere il numero di volte in cui un argomento o un commento deve essere contrassegnato prima di essere nascosto dalla visualizzazione pubblica. Se è impostato su -1, l&#39;argomento o il commento contrassegnato non viene mai nascosto. Altrimenti, questo numero deve essere maggiore o uguale alla soglia di moderazione. Il valore predefinito è 5.

#### Scheda Campo tag {#tag-field-tab}

Sotto **[!UICONTROL Campo tag]** , i tag che possono essere applicati, se consentito dalla scheda **[!UICONTROL Impostazioni]** , sono limitati in base agli spazi dei nomi scelti.

* **Namespace consentiti**

  Pertinente se `Allow Tagging` è controllato nella sezione **[!UICONTROL Impostazioni]** scheda. I tag che possono essere applicati sono limitati a quelli all’interno delle categorie dello spazio dei nomi selezionate. L’elenco degli spazi dei nomi include &quot;Tag standard&quot; (lo spazio dei nomi predefinito) e &quot;Includi tutti i tag&quot;. L’impostazione predefinita non è selezionata, il che significa che tutti gli spazi dei nomi sono consentiti.

* **Limite di suggerimenti**

  Immettere il numero di tag da visualizzare come suggerimento per la pubblicazione del membro nel forum. Un valore di **-1** significa nessun limite. Il valore predefinito è 0.

#### Scheda Impostazioni ordinamento {#sort-settings-tab}

Sotto **[!UICONTROL Impostazioni di ordinamento]** , specificare l&#39;ordinamento dei commenti inviati quando vengono visualizzati.

* **Ordina per**

  Seleziona tutte le selezioni di ordinamento consentite: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. Il valore predefinito è `Newest, Oldest, Last Updated`.

* **Imposta come predefinito**

  Tirare verso il basso per selezionare una delle opzioni di ordinamento selezionate da visualizzare come impostazione predefinita. Il valore predefinito è `Newest`.

* **Seleziona le opzioni di tempo per l&#39;ordinamento Analytics**

  Tirare verso il basso per selezionare uno dei `All, Last 24 Hours, Last 7 Days, Last 30 Days`. Il valore predefinito è `All`.

## Esperienza visitatore del sito {#site-visitor-experience}

### Creazione di un’idea {#creating-idea}

Come per tutte le funzioni di Communities, se non hai effettuato l’accesso, un visitatore del sito può solo leggere idee e visualizzare altre opinioni (tramite commenti e voto/gradimento).

Una volta effettuato l’accesso, un membro può creare un’idea.

![create-new-idea](assets/create-new-idea.png)

Prima di inviare l’idea, il membro può salvare una bozza.

Selezionando `Save as Draft` viene salvata una bozza.

![idea-salvataggio](assets/save-idea.png)

Quando si visualizzano le bozze salvate in `My Drafts` , seleziona `Read More` per riattivare la modalità di modifica:

![edit-idea](assets/edit-idea.png)

#### Invio di feedback {#providing-feedback}

Una volta pubblicata l’idea, gli altri membri possono accedervi e aprirla ( `Read More`) e apprezza l&#39;idea, contribuendo così al conteggio dei voti, e formula commenti.

![feedback](assets/feedback-idea.png)

### Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili sul sito [Ideation Essentials](/help/communities/ideation.md) pagina per sviluppatori.

Per la moderazione degli argomenti e dei commenti pubblicati, vedi [Moderazione dei contenuti generati dagli utenti](/help/communities/moderate-ugc.md).

Per assegnare tag agli argomenti e ai commenti pubblicati, consulta [Assegnazione di tag ai contenuti generati dagli utenti](/help/communities/tag-ugc.md).
