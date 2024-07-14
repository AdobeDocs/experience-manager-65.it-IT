---
title: Funzione ideazione
description: Scopri come aggiungere e configurare la funzione di ideazione che consente ai membri della community di creare, visualizzare, seguire, votare e commentare le idee condivise con la community.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: e130bab4-524d-4413-ba8b-53d0ed9e8623
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 0%

---

# Funzione ideazione {#ideation-feature}

## Introduzione {#introduction}

La funzione di ideazione fornisce un’area per i visitatori del sito connessi (membri della community) nell’ambiente Publish per:

* Creare idee da condividere con la community.
* Visualizzare e commentare le idee.
* Segui un&#39;idea.
* Votate un&#39;idea.

Questa sezione della documentazione descrive:

* Aggiunta della funzione di ideazione a un sito AEM.
* Impostazioni di configurazione del componente Ideazione.

### Aggiunta di un’idea a una pagina {#adding-a-ideation-to-a-page}

Per aggiungere un componente `Ideation` a una pagina in modalità di creazione, utilizza il browser componenti per individuare

* `Communities / Ideation`

Trascinarlo nella posizione desiderata su una pagina in cui dovrebbe essere visualizzata l&#39;idea.

Per informazioni necessarie, visitare [Nozioni di base sui componenti delle community](/help/communities/basics.md).

Quando sono incluse le [librerie lato client richieste](/help/communities/ideation.md#essentials-for-client-side), il componente `Ideation` viene visualizzato in questo modo:

![ideazione](assets/ideation.png)

### Configurazione di un’idea {#configuring-an-ideation}

Selezionare il componente `Ideation` inserito in modo da poter accedere e selezionare l&#39;icona `Configure` che apre la finestra di dialogo per modifica.

![configura-nuovo](assets/configure-new.png)

![ideation-settings](assets/ideation-settings.png)

#### Scheda Impostazioni {#settings-tab}

Nella scheda **[!UICONTROL Impostazioni]**, specifica le impostazioni per idee e commenti:

* **Consenti miniatura allegato**
* **Dimensione massima miniatura allegato**
* **Dimensioni minime immagine per miniatura**
* **Dimensione massima miniatura**
* **Consenti membri privilegiati**
* **Membri privilegiati consentiti**
* **Blocca contenuto generato dall&#39;utente in modalità Modifica autore**
* **Titolo ideazione**

* Titolo visualizzato dell&#39;idea. Il valore predefinito è `Ideation`.
* **Descrizione ideazione**

  Descrizione da visualizzare come sottotitolo dell&#39;idea. Il valore predefinito non è una descrizione.

* **Argomenti per pagina**

  Definisce il numero di idee/post mostrati per pagina. Il valore predefinito è 10.

* **Moderato**

  Se questa opzione è selezionata, è necessario approvare la pubblicazione di idee e commenti prima di visualizzarli in un sito pubblicato. L&#39;impostazione predefinita è deselezionata.

* **Chiuso**

  Se questa opzione è selezionata, il forum di ideazione è chiuso a nuove idee e commenti. L&#39;impostazione predefinita è deselezionata.

* **Editor Rich Text**

  Se questa opzione è selezionata, è possibile immettere idee e commenti con il markup. L&#39;impostazione predefinita è deselezionata.

* **Consenti assegnazione tag**

  Se questa opzione è selezionata, consentire ai membri di aggiungere etichette tag ai propri post (vedere la scheda **[!UICONTROL Campo tag]**). L&#39;impostazione predefinita è deselezionata.

* **Consenti caricamenti file**

  Se questa opzione è selezionata, consenti l&#39;aggiunta di file allegati all&#39;idea o al commento. L&#39;impostazione predefinita è deselezionata.

* **Dimensione massima file**

  Rilevante solo se è selezionato `Allow File Uploads`. Questo campo limita la dimensione (in byte) di un file caricato. Il valore predefinito è 104857600 (10 Mb).

* **Tipi di file consentiti**

  Rilevante solo se è selezionato `Allow File Uploads`. Un elenco separato da virgole di estensioni di file con il separatore &quot;punto&quot;. Ad esempio, .jpg, .jpeg, .png, .doc, .docx, .pdf. Se sono specificati dei tipi di file, non è possibile caricare quelli non specificati. Il valore predefinito è none specificato, pertanto tutti i tipi di file sono consentiti.

* **Dimensione massima file immagine allegato**

  Rilevante solo se è selezionata l’opzione Consenti caricamenti file. Numero massimo di byte consentito per un file di immagine caricato. Il valore predefinito è 2097152 (2 Mb).

* **Consenti risposte**

  Se questa opzione è selezionata, consenti le risposte ai commenti inviati all&#39;idea. L&#39;impostazione predefinita è deselezionata.

* **Consenti votazione**

  Se questa opzione è selezionata, consentire la votazione dei commenti di un&#39;idea. L&#39;impostazione predefinita è deselezionata.

* **Consenti agli utenti di eliminare commenti e argomenti**

  Se questa opzione è selezionata, consentire ai membri di eliminare i commenti e le idee pubblicati. L&#39;impostazione predefinita è deselezionata.

* **Consenti Segui**

  Se questa opzione è selezionata, includere la seguente funzionalità per i post di idea, che consente ai membri di ricevere [notifica](/help/communities/notifications.md) dei nuovi post. L&#39;impostazione predefinita è deselezionata.

* **Consenti iscrizioni e-mail**

  Se questa opzione è selezionata, consenti ai membri di ricevere notifiche sui nuovi post tramite e-mail ([abbonamento](/help/communities/subscriptions.md)). Richiede `Allow Following` per essere controllato e [configurato](/help/communities/email.md). L&#39;impostazione predefinita è deselezionata.

* **Consenti votazione**

  Se questa opzione è selezionata, consentire la votazione dei commenti di un&#39;idea. L&#39;impostazione predefinita è deselezionata.

* **Distintivi visualizzati**

  Se questa opzione è selezionata, vengono visualizzati i [distintivi](/help/communities/implementing-scoring.md) ottenuti e assegnati con l&#39;idea di un membro. L&#39;impostazione predefinita è deselezionata.

* **Non ricevere risposte nella pagina dell&#39;elenco**

* **Consenti contenuto in primo piano**

  Se questa opzione è selezionata, l&#39;idea è identificabile come [contenuto in primo piano](/help/communities/featured.md). L&#39;impostazione predefinita è deselezionata.

* **Abilita menzione**
* **Max menzioni**
* **Pattern menzioni interfaccia utente**

#### Scheda Moderazione utente {#user-moderation-tab}

Nella scheda **[!UICONTROL Moderazione utente]**, specifica come vengono gestiti le idee e i commenti pubblicati (contenuti generati dall&#39;utente). Per ulteriori informazioni, vedere [Moderazione del contenuto generato dall&#39;utente](/help/communities/moderate-ugc.md).

* **Rifiuta post**

  Se questa opzione è selezionata, i moderatori membri di fiducia possono negare i post e impedirne la visualizzazione nel forum pubblico. L&#39;impostazione predefinita è deselezionata.

* **Chiudi/Riapri argomenti**

  Se questa opzione è selezionata, i moderatori membri attendibili possono chiudere un argomento per ulteriori modifiche e commenti e riaprire un argomento. L&#39;impostazione predefinita è deselezionata.

* **Contrassegna post**

  Se questa opzione è selezionata, consentire ai membri di contrassegnare gli argomenti o i commenti di altri utenti come non appropriati. L&#39;impostazione predefinita è deselezionata.

* **Elenco motivi contrassegno**

  Se questa opzione è selezionata, consentire ai membri di scegliere, da un elenco a discesa, il motivo per cui contrassegnare un argomento o un commento come non appropriato. L&#39;impostazione predefinita è deselezionata.

* **Motivo contrassegno personalizzato**

  Se questa opzione è selezionata, consentire ai membri di immettere un motivo specifico per contrassegnare un argomento o un commento come non appropriato. L&#39;impostazione predefinita è deselezionata.

* **Soglia moderazione**

  Immettere il numero di volte in cui un argomento o un commento deve essere segnalato dai membri prima che il moderatore riceva una notifica. Il valore predefinito è 1 (una tantum).

* **Limite di segnalazione**

  Immettere il numero di volte in cui un argomento o un commento deve essere contrassegnato prima di essere nascosto dalla visualizzazione pubblica. Se è impostato su -1, l&#39;argomento o il commento contrassegnato non viene mai nascosto. Altrimenti, questo numero deve essere maggiore o uguale alla soglia di moderazione. Il valore predefinito è 5.

#### Scheda Campo tag {#tag-field-tab}

Nella scheda **[!UICONTROL Campo tag]**, i tag che possono essere applicati, se consentiti nella scheda **[!UICONTROL Impostazioni]**, sono limitati in base agli spazi dei nomi scelti.

* **Spazi dei nomi consentiti**

  Rilevante se `Allow Tagging` è selezionato nella scheda **[!UICONTROL Impostazioni]**. I tag che possono essere applicati sono limitati a quelli all’interno delle categorie dello spazio dei nomi selezionate. L’elenco degli spazi dei nomi include &quot;Tag standard&quot; (lo spazio dei nomi predefinito) e &quot;Includi tutti i tag&quot;. L’impostazione predefinita non è selezionata, il che significa che tutti gli spazi dei nomi sono consentiti.

* **Limite suggerimenti**

  Immettere il numero di tag da visualizzare come suggerimento per la pubblicazione del membro nel forum. Un valore compreso tra **e 1** non indica alcun limite. Il valore predefinito è 0.

#### Scheda Impostazioni ordinamento {#sort-settings-tab}

Nella scheda **[!UICONTROL Impostazioni ordinamento]**, specifica l&#39;ordinamento dei commenti inviati quando vengono visualizzati.

* **Ordina per**

  Controllare tutte le selezioni di ordinamento consentite: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. Il valore predefinito è `Newest, Oldest, Last Updated`.

* **Imposta come predefinito**

  Tirare verso il basso per selezionare una delle opzioni di ordinamento selezionate da visualizzare come impostazione predefinita. Il valore predefinito è `Newest`.

* **Selezionare le opzioni di tempo per l&#39;ordinamento di Analytics**

  Tirare verso il basso per selezionare uno di `All, Last 24 Hours, Last 7 Days, Last 30 Days`. Il valore predefinito è `All`.

## Esperienza visitatore del sito {#site-visitor-experience}

### Creazione di un’idea {#creating-idea}

Come per tutte le funzioni di Communities, se non hai effettuato l’accesso, un visitatore del sito può solo leggere idee e visualizzare altre opinioni (tramite commenti e voto/gradimento).

Una volta effettuato l’accesso, un membro può creare un’idea.

![create-new-idea](assets/create-new-idea.png)

Prima di inviare l’idea, il membro può salvare una bozza.

Selezionando il pulsante `Save as Draft`, viene salvata una bozza.

![idea salvata](assets/save-idea.png)

Quando si visualizzano le bozze salvate nella scheda `My Drafts`, selezionare `Read More` per riattivare la modalità di modifica:

![idea-modifica](assets/edit-idea.png)

#### Invio di feedback {#providing-feedback}

Dopo la pubblicazione dell&#39;idea, gli altri membri potranno accedere, aprire l&#39;idea ( `Read More`) e aggiungerla al conteggio dei voti e aggiungere commenti.

![feedback](assets/feedback-idea.png)

### Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Ideation Essentials](/help/communities/ideation.md) per sviluppatori.

Per la moderazione degli argomenti e dei commenti pubblicati, vedere [Moderazione del contenuto generato dall&#39;utente](/help/communities/moderate-ugc.md).

Per assegnare tag agli argomenti e ai commenti pubblicati, vedere [Assegnazione di tag ai contenuti generati dagli utenti](/help/communities/tag-ugc.md).
