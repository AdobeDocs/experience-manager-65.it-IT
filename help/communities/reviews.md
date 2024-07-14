---
title: Utilizzo di recensioni e riepilogo recensioni (visualizzazione)
description: Scopri come aggiungere i componenti Recensioni e Riepilogo recensioni a una pagina.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 170414a6-c40b-4ad2-9294-7c2266850c3d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 0%

---

# Utilizzo di recensioni e riepilogo recensioni (visualizzazione) {#using-reviews-and-reviews-summary-display}

Il componente `Reviews` è un composito di [Commenti](comments.md) e [Valutazione](rating.md) componenti pronti per l&#39;uso.

Il componente `Reviews Summary (Display)` fornisce un riepilogo di un&#39;istanza attiva o chiusa di un componente `Reviews` per la visualizzazione in altre aree del sito.

>[!NOTE]
>
>La pubblicazione anonima di una revisione non è supportata. I visitatori del sito devono registrarsi (diventare membri) e accedere per partecipare. Il visitatore che ha effettuato l’accesso può aggiornare la propria revisione in qualsiasi momento.

## Aggiunta di una revisione a una pagina {#adding-a-review-to-a-page}

Per aggiungere un componente `Reviews` a una pagina in modalità di creazione, utilizzare il browser componenti per individuare `Communities / Reviews` e trascinarlo in una pagina, ad esempio una posizione relativa alla caratteristica da rivedere per gli utenti.

Per informazioni necessarie, visitare [Nozioni di base sui componenti delle community](basics.md).

Quando sono incluse le [librerie lato client richieste](reviews-basics.md#essentials-for-client-side), il componente `Reviews` viene visualizzato in questo modo.

![crea-revisione](assets/create-review.png)

## Configurazione delle recensioni {#configuring-reviews}

Selezionare il componente `Reviews` inserito in modo da poter accedere e selezionare l&#39;icona `Configure` che apre la finestra di dialogo per modifica.

![configura-nuovo](assets/configure-new.png)

Nella scheda **[!UICONTROL Classificazioni consentite]** specificare l&#39;elenco completo delle classificazioni da mostrare ai membri. La prima valutazione deve essere generale, in quanto è la valutazione che fornisce la valutazione media per il componente `Review Summary (Display)`. Alle due valutazioni successive nella configurazione predefinita deve essere assegnato un titolo diverso, diverso da &quot;Subrazione 1&quot; o &quot;Subrazione 2&quot;.

![valutazione consentita](assets/configure-review1.png)

* **[!UICONTROL Classificazioni consentite]**

  Un elenco di valutazioni tra cui un membro può scegliere.

  Utilizzare la freccia su, la freccia giù e i pulsanti di eliminazione per modificare le selezioni visibili.

  Fai clic su **[!UICONTROL Aggiungi elemento]** per aggiungere un&#39;altra scelta di valutazione.

Nella scheda **[!UICONTROL Classificazioni richieste]**, reimmettere gli elementi dall&#39;elenco di **[!UICONTROL Classificazioni consentite]** necessari per la classificazione. Se un elemento viene specificato solo nella scheda Classificazioni consentite, può non essere contrassegnato quando viene inviato dal membro.

Sul sito web, le valutazioni richieste sono contrassegnate da un asterisco. Se un elemento è obbligatorio e non è contrassegnato, viene visualizzato un messaggio per il membro e l&#39;invio viene negato fino a quando tutte le valutazioni richieste non vengono contrassegnate.

![classificazione richiesta](assets/configure-review2.png)

* **[!UICONTROL Classificazioni richieste]**

  Un sottoinsieme di valutazioni consentite, che indica quali valutazioni sono richieste.

  Utilizzare la freccia su, la freccia giù e i pulsanti di eliminazione per modificare le selezioni visibili.

  Fai clic su **[!UICONTROL Aggiungi elemento]** per aggiungere un&#39;altra scelta di risposta.

>[!NOTE]
>
>Se un elemento viene immesso nella scheda **[!UICONTROL Classificazioni richieste]** non specificata nella scheda **[!UICONTROL Classificazioni consentite]**, non verrà incluso negli elementi da valutare.

Nella scheda **[!UICONTROL Recensioni]**, specifica come vengono gestite le revisioni.

![recensioni](assets/configure-review3.png)

* **[!UICONTROL Consenti risposte]**

  Se questa opzione è selezionata, consenti le risposte alle revisioni. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Chiuso]**

  Se questa opzione è selezionata, la revisione verrà chiusa alle nuove revisioni e risposte. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Consenti caricamenti file]**

  Se questa opzione è selezionata, consenti il caricamento degli allegati per la revisione. L&#39;impostazione predefinita è deselezionata.

* **Dimensione massima file**

  Rilevante solo se è selezionato **[!UICONTROL Consenti caricamenti file]**. Questo campo limita la dimensione (in byte) di un file caricato. Il valore predefinito è 10 MB.

* **[!UICONTROL Lunghezza massima messaggio]**

  Numero massimo di caratteri che possono essere immessi nella casella di testo. Il valore predefinito è 4096 caratteri.

* **[!UICONTROL Tipi di file consentiti]**

  Rilevante solo se è selezionato **[!UICONTROL Consenti caricamenti file]**. Un elenco separato da virgole di estensioni di file con il separatore &quot;punto&quot;. Ad esempio, .jpg, .jpeg, .png, .doc, .docx, .pdf. Se sono specificati tipi di file, quelli non specificati non sono consentiti. Il valore predefinito è none specificato, pertanto tutti i tipi di file sono consentiti.

* **[!UICONTROL Editor Rich Text]**

  Se questa opzione è selezionata, i post possono essere immessi con markup. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Consenti votazione]**

  Se questa opzione è selezionata, includere la funzionalità di votazione per un argomento. L&#39;impostazione predefinita è deselezionata.

Nella scheda **[!UICONTROL Moderazione utente]**, specifica come vengono gestite le recensioni pubblicate. Per ulteriori informazioni, vedere [Moderazione del contenuto generato dall&#39;utente](moderate-ugc.md).

![moderazione utente](assets/configure-review4.png)

* **[!UICONTROL Pre-moderazione]**

  Se questa opzione è selezionata, le recensioni devono essere approvate prima di essere visualizzate su un sito pubblicato. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Elimina recensioni]**

  Se questa opzione è selezionata, il membro che ha pubblicato la revisione può eliminarla. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Rifiuta recensioni]**

  Se questa opzione è selezionata, consenti ai moderatori di rifiutare le recensioni. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Chiudi/Riapri recensioni]**

  Se questa opzione è selezionata, consenti ai moderatori di chiudere e riaprire le recensioni. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Segnala recensioni]**

  Se questa opzione è selezionata, consenti ai membri di segnalare le revisioni non appropriate. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Elenco motivi contrassegno]**

  Se questa opzione è selezionata, consentire ai membri di scegliere, da un elenco a discesa, il motivo per cui contrassegnare una revisione come inappropriata. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Motivo contrassegno personalizzato]**

  Se questa opzione è selezionata, consentire ai membri di immettere il proprio motivo per contrassegnare una revisione come inappropriata. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Soglia moderazione]**

  Immetti il numero di volte in cui i membri devono segnalare una revisione prima che il moderatore riceva una notifica. Il valore predefinito è una tantum (1).

* **[!UICONTROL Limite di segnalazione]**

  Immettere il numero di volte in cui è necessario contrassegnare una revisione prima che venga nascosta alla visualizzazione pubblica. Questo numero deve essere maggiore o uguale alla **[!UICONTROL soglia di moderazione]**. Il valore predefinito è 5.

### Aggiunta di un riepilogo di revisione (visualizzazione) a una pagina {#adding-a-review-summary-display-to-a-page}

Per aggiungere un componente `Reviews Summary (Display)` a una pagina in modalità di creazione, individua il componente

* `Communities / Reviews Summary (Display)`

Trascinarlo in una pagina in cui deve essere visualizzato un riepilogo di una revisione attiva o chiusa.

Per informazioni necessarie, visitare [Nozioni di base sui componenti delle community](basics.md).

Quando sono incluse le [librerie lato client richieste](reviews-basics.md#essentials-for-client-side), il componente `Reviews Summary (Display)` viene visualizzato in questo modo.

![revisione-riepilogo](assets/configure-review5.png)

>[!NOTE]
>
>La &quot;Media&quot; riflette i voti per il primo elemento elencato nelle schede Classificazioni consentite della revisione in fase di riepilogo.

### Configurazione del riepilogo delle recensioni (visualizzazione) {#configuring-reviews-summary-display}

Selezionare il componente `Reviews Summary (Display)` inserito in modo da poter accedere e selezionare l&#39;icona `Configure` che apre la finestra di dialogo per modifica.

![configura](assets/configure-new.png)

Nella scheda **[!UICONTROL Riepilogo recensioni]**

![revisione-riepilogo](assets/configure-review6.png)

* `Review Path`

  Immettere o passare all&#39;istanza inserita del componente `reviews` in modo da poter riepilogare, ad esempio, se aggiunto alla pagina Web del sito [Geometrixx Engage](getting-started.md), il percorso sarà:

  `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

  Se questa opzione è selezionata, includi la visualizzazione di un grafico a barre indicante quante stelle di valutazione sono presenti nelle recensioni riepilogate. L&#39;impostazione predefinita è deselezionata.

### Passaggio a un tipo di revisione personalizzato {#changing-to-a-custom-review-type}

Il componente Recensioni utilizza il sistema di commenti.

Modificando il tipo di risorsa Commento, il sistema dei commenti non genera più un&#39;istanza di un commento utilizzando l&#39;impostazione predefinita, ma una che è stata personalizzata (estesa) dagli sviluppatori.

Quando i tipi di risorse personalizzati sono noti, immettere [Modalità progettazione](../../help/sites-authoring/default-components-designmode.md) e fare doppio clic sul componente `Comments` inserito per aprire una finestra di dialogo con una scheda aggiuntiva.

Nella scheda **[!UICONTROL Tipi di risorse]**, specificare il tipo di risorsa personalizzato per le nuove istanze dei componenti `Comments or Voting`:

![commenti-voto](assets/configure-review7.png)

* **[!UICONTROL Tipo risorsa commento]**

  Passare alla classe resourceType di un componente `comment` esteso (commento singolo) in /apps. Esempio: `/apps/social/commons/components/hbs/comments/comment`.

  Questa risorsa identifica il resourceType del UGC creato quando un visitatore pubblica un commento.

* **[!UICONTROL Tipo risorsa voto]**

  Passare alla classe resourceType di un componente `voting` esteso in /apps. Esempio: `/apps/social/components/hbs/voting`.

  Questa risorsa identifica il tipo di risorsa dell’UGC creato quando un visitatore pubblica un voto.

* **[!UICONTROL Tipo risorsa sistema commenti]**

  Passare alla classe resourceType di un componente `comments` esteso (sistema di commenti) in /apps. Lasciare vuoto a meno che il modello di pagina [includa dinamicamente](scf.md#add-or-include-a-communities-component) il sistema di commenti nello script sottostante anziché essere aggiunto alla pagina come risorsa (nodo commenti). Ulteriori informazioni sull&#39;helper [`{{include}}`](handlebars-helpers.md#include).

## Esperienza visitatore del sito {#site-visitor-experience}

### Moderatori e amministratori {#moderators-and-administrators}

Quando l&#39;utente connesso dispone dei privilegi di moderatore o amministratore, può eseguire le attività di moderazione consentite dalla configurazione del componente, indipendentemente da chi ha creato la revisione.

### Membri {#members}

Quando il visitatore del sito ha effettuato l’accesso, a seconda della configurazione, può:

* Post: una nuova recensione
* Modifica la propria recensione
* Elimina la propria recensione
* Contrassegna i commenti di revisione di altri utenti

È consentita una sola valutazione per membro. L&#39;iscritto può cambiare la propria valutazione in qualsiasi momento.

### Anonimo {#anonymous}

I visitatori del sito che non hanno effettuato l&#39;accesso possono solo leggere le recensioni postate, tradurle se supportate, ma non possono aggiungere una valutazione o una revisione, né segnalare i commenti di revisione di altri utenti.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Rivedi Essentials](reviews-basics.md) per sviluppatori.

Per la moderazione dei commenti pubblicati, vedere [Moderazione del contenuto generato dall&#39;utente](moderate-ugc.md).

Per la traduzione dei commenti pubblicati, vedere [Traduzione del contenuto generato dall&#39;utente](translate-ugc.md).
