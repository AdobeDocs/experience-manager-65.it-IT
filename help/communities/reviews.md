---
title: Utilizzo di recensioni e riepilogo recensioni (visualizzazione)
description: Scopri come aggiungere i componenti Recensioni e Riepilogo recensioni a una pagina.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 170414a6-c40b-4ad2-9294-7c2266850c3d
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '1285'
ht-degree: 4%

---

# Utilizzo di recensioni e riepilogo recensioni (visualizzazione) {#using-reviews-and-reviews-summary-display}

Il `Reviews` il componente è un composito di [Commenti](comments.md) e [Valutazione](rating.md) componenti pronti per l’uso.

Il `Reviews Summary (Display)` componente fornisce un riepilogo di un&#39;istanza attiva o chiusa di un `Reviews` componente da visualizzare altrove sul sito.

>[!NOTE]
>
>La pubblicazione anonima di una revisione non è supportata. I visitatori del sito devono registrarsi (diventare membri) e accedere per partecipare. Il visitatore che ha effettuato l’accesso può aggiornare la propria revisione in qualsiasi momento.

## Aggiunta di una revisione a una pagina {#adding-a-review-to-a-page}

Per aggiungere una `Reviews` a una pagina in modalità di authoring, utilizza il browser Componenti per individuare `Communities / Reviews` e trascinarlo nella posizione desiderata su una pagina, ad esempio una posizione relativa alla caratteristica da rivedere.

Per informazioni necessarie, visitare il sito [Nozioni di base sui componenti community](basics.md).

Quando [librerie lato client richieste](reviews-basics.md#essentials-for-client-side) sono inclusi, è così che `Reviews` viene visualizzato.

![create-review](assets/create-review.png)

## Configurazione delle recensioni {#configuring-reviews}

Seleziona la inserita `Reviews` in modo da poter accedere e selezionare `Configure` che apre la finestra di dialogo per modifica.

![configure-new](assets/configure-new.png)

Sotto **[!UICONTROL Classificazioni consentite]** , specificare l&#39;elenco completo delle valutazioni da mostrare ai membri. Il primo rating dovrebbe essere generale, poiché è il rating che fornisce il rating medio per il `Review Summary (Display)` componente. Alle due valutazioni successive nella configurazione predefinita deve essere assegnato un titolo diverso, diverso da &quot;Subrazione 1&quot; o &quot;Subrazione 2&quot;.

![valutazione consentita](assets/configure-review1.png)

* **[!UICONTROL Classificazioni consentite]**

  Un elenco di valutazioni tra cui un membro può scegliere.

  Utilizzare la freccia su, la freccia giù e i pulsanti di eliminazione per modificare le selezioni visibili.

  Clic **[!UICONTROL Aggiungi elemento]** per aggiungere un’altra scelta di valutazione.

Sotto **[!UICONTROL Classificazioni richieste]** , reinserisci gli elementi dall&#39;elenco di **[!UICONTROL Classificazioni consentite]** necessari per la valutazione. Se un elemento viene specificato solo nella scheda Classificazioni consentite, può non essere contrassegnato quando viene inviato dal membro.

Sul sito web, le valutazioni richieste sono contrassegnate da un asterisco. Se un elemento è obbligatorio e non è contrassegnato, viene visualizzato un messaggio per il membro e l&#39;invio viene negato fino a quando tutte le valutazioni richieste non vengono contrassegnate.

![classificazione richiesta](assets/configure-review2.png)

* **[!UICONTROL Classificazioni richieste]**

  Un sottoinsieme di valutazioni consentite, che indica quali valutazioni sono richieste.

  Utilizzare la freccia su, la freccia giù e i pulsanti di eliminazione per modificare le selezioni visibili.

  Clic **[!UICONTROL Aggiungi elemento]** per aggiungere un’altra scelta di risposta.

>[!NOTE]
>
>Se un articolo viene immesso sul **[!UICONTROL Classificazioni richieste]** scheda non specificata nella **[!UICONTROL Classificazioni consentite]** , non è incluso negli elementi da valutare.

Sotto **[!UICONTROL Recensioni]** , specificare la modalità di gestione delle revisioni.

![recensioni](assets/configure-review3.png)

* **[!UICONTROL Consenti risposte]**

  Se questa opzione è selezionata, consenti le risposte alle revisioni. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Chiuso]**

  Se questa opzione è selezionata, la revisione verrà chiusa alle nuove revisioni e risposte. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Consenti caricamenti file]**

  Se questa opzione è selezionata, consenti il caricamento degli allegati per la revisione. L&#39;impostazione predefinita è deselezionata.

* **Dimensione file massima**

  Rilevante solo se **[!UICONTROL Consenti caricamenti file]** è selezionato. Questo campo limita la dimensione (in byte) di un file caricato. Il valore predefinito è 10 MB.

* **[!UICONTROL Lunghezza massima messaggio]**

  Numero massimo di caratteri che possono essere immessi nella casella di testo. Il valore predefinito è 4096 caratteri.

* **[!UICONTROL Tipi di file consentiti]**

  Rilevante solo se **[!UICONTROL Consenti caricamenti file]** è selezionato. Un elenco separato da virgole di estensioni di file con il separatore &quot;punto&quot;. Ad esempio, .jpg, .jpeg, .png, .doc, .docx, .pdf. Se sono specificati tipi di file, quelli non specificati non sono consentiti. Il valore predefinito è none specificato, pertanto tutti i tipi di file sono consentiti.

* **[!UICONTROL Editor Rich Text]**

  Se questa opzione è selezionata, i post possono essere immessi con markup. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Consenti votazione]**

  Se questa opzione è selezionata, includere la funzionalità di votazione per un argomento. L&#39;impostazione predefinita è deselezionata.

Sotto **[!UICONTROL Moderazione utenti]** , specifica come vengono gestite le recensioni postate. Per ulteriori informazioni, consulta [Moderazione dei contenuti generati dagli utenti](moderate-ugc.md).

![moderazione utente](assets/configure-review4.png)

* **[!UICONTROL Premoderazione]**

  Se questa opzione è selezionata, le recensioni devono essere approvate prima di essere visualizzate su un sito pubblicato. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Elimina recensioni]**

  Se questa opzione è selezionata, il membro che ha pubblicato la revisione può eliminarla. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Rifiuta recensioni]**

  Se questa opzione è selezionata, consenti ai moderatori di rifiutare le recensioni. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Chiudi/Riapri recensioni]**

  Se questa opzione è selezionata, consenti ai moderatori di chiudere e riaprire le recensioni. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Segnala recensioni]**

  Se questa opzione è selezionata, consenti ai membri di segnalare le revisioni non appropriate. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Elenco di motivi per segnalazione]**

  Se questa opzione è selezionata, consentire ai membri di scegliere, da un elenco a discesa, il motivo per cui contrassegnare una revisione come inappropriata. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Motivo per segnalazione personalizzato]**

  Se questa opzione è selezionata, consentire ai membri di immettere il proprio motivo per contrassegnare una revisione come inappropriata. L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Soglia moderazione]**

  Immetti il numero di volte in cui i membri devono segnalare una revisione prima che il moderatore riceva una notifica. Il valore predefinito è una tantum (1).

* **[!UICONTROL Limite segnalazione]**

  Immettere il numero di volte in cui è necessario contrassegnare una revisione prima che venga nascosta alla visualizzazione pubblica. Questo numero deve essere maggiore o uguale al **[!UICONTROL Soglia moderazione]**. Il valore predefinito è 5.

### Aggiunta di un riepilogo di revisione (visualizzazione) a una pagina {#adding-a-review-summary-display-to-a-page}

Per aggiungere una `Reviews Summary (Display)` a una pagina in modalità di authoring, individua il componente

* `Communities / Reviews Summary (Display)`

Trascinarlo in una pagina in cui deve essere visualizzato un riepilogo di una revisione attiva o chiusa.

Per informazioni necessarie, visitare il sito [Nozioni di base sui componenti community](basics.md).

Quando [librerie lato client richieste](reviews-basics.md#essentials-for-client-side) sono inclusi, è così che `Reviews Summary (Display)`viene visualizzato.

![review-summary](assets/configure-review5.png)

>[!NOTE]
>
>La &quot;Media&quot; riflette i voti per il primo elemento elencato nelle schede Classificazioni consentite della revisione in fase di riepilogo.

### Configurazione del riepilogo delle recensioni (visualizzazione) {#configuring-reviews-summary-display}

Seleziona la inserita `Reviews Summary (Display)` in modo da poter accedere e selezionare `Configure` che apre la finestra di dialogo per modifica.

![configura](assets/configure-new.png)

Sotto **[!UICONTROL Riepilogo recensioni]** scheda

![review-summary](assets/configure-review6.png)

* `Review Path`

  Inserisci o sfoglia l’istanza inserita del `reviews` componente che consente di riepilogare, ad esempio, se aggiunto alla pagina web del [Geometrixx sito di coinvolgimento,](getting-started.md) il percorso sarà:

  `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

  Se questa opzione è selezionata, includi la visualizzazione di un grafico a barre indicante quante stelle di valutazione sono presenti nelle recensioni riepilogate. L&#39;impostazione predefinita è deselezionata.

### Passaggio a un tipo di revisione personalizzato {#changing-to-a-custom-review-type}

Il componente Recensioni utilizza il sistema di commenti.

Modificando il tipo di risorsa Commento, il sistema dei commenti non genera più un&#39;istanza di un commento utilizzando l&#39;impostazione predefinita, ma una che è stata personalizzata (estesa) dagli sviluppatori.

Quando sono noti i tipi di risorse personalizzati, immetti [Modalità Progettazione](../../help/sites-authoring/default-components-designmode.md) e fare doppio clic sul `Comments` per aprire una finestra di dialogo con una scheda aggiuntiva.

Sotto **[!UICONTROL Tipi di risorse]** , specificare il resourceType personalizzato per le nuove istanze del `Comments or Voting` componenti:

![commenti-votazione](assets/configure-review7.png)

* **[!UICONTROL Tipo risorsa commento]**

  Passare al resourceType di un&#39;estensione `comment`componente (commento singolo) in /apps. Esempio: `/apps/social/commons/components/hbs/comments/comment`.

  Questa risorsa identifica il resourceType del UGC creato quando un visitatore pubblica un commento.

* **[!UICONTROL Tipo di risorsa per votazione]**

  Passare al resourceType di un&#39;estensione `voting`componente in /apps. Esempio: `/apps/social/components/hbs/voting`.

  Questa risorsa identifica il tipo di risorsa dell’UGC creato quando un visitatore pubblica un voto.

* **[!UICONTROL Tipo risorsa sistema commenti]**

  Passare al resourceType di un&#39;estensione `comments`componente (sistema di commenti) in /apps. Lascia vuoto a meno che il modello della pagina non sia [include in modo dinamico](scf.md#add-or-include-a-communities-component) il sistema di commenti nello script sottostante, anziché essere aggiunto alla pagina come risorsa (nodo commenti). Per saperne di più leggi le [`{{include}}` aiutante](handlebars-helpers.md#include).

## Esperienza visitatore del sito {#site-visitor-experience}

### Moderatori e amministratori {#moderators-and-administrators}

Quando l&#39;utente connesso dispone dei privilegi di moderatore o amministratore, può eseguire le attività di moderazione consentite dalla configurazione del componente, indipendentemente da chi ha creato la revisione.

### Membri {#members}

Quando il visitatore del sito ha effettuato l’accesso, a seconda della configurazione, può:

* Pubblica una nuova recensione
* Modifica la propria recensione
* Elimina la propria recensione
* Contrassegna i commenti di revisione di altri utenti

È consentita una sola valutazione per membro. L&#39;iscritto può cambiare la propria valutazione in qualsiasi momento.

### Anonimo {#anonymous}

I visitatori del sito che non hanno effettuato l&#39;accesso possono solo leggere le recensioni postate, tradurle se supportate, ma non possono aggiungere una valutazione o una revisione, né segnalare i commenti di revisione di altri utenti.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili sul sito [Rivedi elementi di base](reviews-basics.md) pagina per sviluppatori.

Per la moderazione dei commenti pubblicati, vedi [Moderazione dei contenuti generati dagli utenti](moderate-ugc.md).

Per la traduzione dei commenti pubblicati, vedi [Traduzione dei contenuti generati dagli utenti](translate-ugc.md).
