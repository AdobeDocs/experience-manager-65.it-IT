---
title: Riepilogo recensioni e revisioni (visualizzazione)
seo-title: Using Reviews and Reviews Summary (Display)
description: Aggiunta dei componenti Riepilogo recensioni e revisioni a una pagina
seo-description: Adding the Reviews and Reviews Summary components to a page
uuid: bd1ccee7-b26b-4a27-b1ea-89609f5080af
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: bf4e7809-8def-4647-aaa6-3ac36865511f
exl-id: 170414a6-c40b-4ad2-9294-7c2266850c3d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 4%

---

# Riepilogo recensioni e revisioni (visualizzazione) {#using-reviews-and-reviews-summary-display}

La `Reviews` un componente è un composito di [Commenti](comments.md) e [Valutazione](rating.md) componenti pronti per l’uso.

La `Reviews Summary (Display)` fornisce un riepilogo di un’istanza attiva o chiusa di un `Reviews` per la visualizzazione in altre aree del sito.

>[!NOTE]
>
>Pubblicazione anonima di una revisione non supportata. I visitatori del sito devono registrarsi (diventare membro) e accedere per partecipare. Il visitatore che ha effettuato l’accesso può aggiornare la propria revisione in qualsiasi momento.

## Aggiunta di una revisione a una pagina {#adding-a-review-to-a-page}

Per aggiungere una `Reviews` componente per una pagina in modalità di creazione, usate il browser componenti per individuare `Communities / Reviews` e trascinarlo nella posizione desiderata su una pagina, ad esempio una posizione relativa alla funzione da rivedere per gli utenti.

Per le informazioni necessarie, visita [Nozioni di base sui componenti di Communities](basics.md).

Quando il [librerie lato client richieste](reviews-basics.md#essentials-for-client-side) sono inclusi, è così che `Reviews` apparirà .

![creazione-revisione](assets/create-review.png)

## Configurazione delle revisioni {#configuring-reviews}

Seleziona il `Reviews` per accedere e selezionare il `Configure` che apre la finestra di dialogo di modifica.

![configure-new](assets/configure-new.png)

Sotto la **[!UICONTROL Valutazioni consentite]** specificare l&#39;elenco completo delle valutazioni da visualizzare ai membri. Il primo rating dovrebbe essere un rating generale/generale, in quanto è il rating che fornisce il rating medio per `Review Summary (Display)` componente. Alle due valutazioni successive nella configurazione predefinita deve essere assegnato un titolo diverso, diverso da &quot;Subrating 1&quot; o &quot;Subrating 2&quot;.

![abilitazione](assets/configure-review1.png)

* **[!UICONTROL Classificazioni consentite]**

   Un elenco di valutazioni da cui un membro può scegliere.

   Utilizzare i pulsanti freccia su, freccia giù ed Elimina per modificare le selezioni visibili.

   Fai clic su **[!UICONTROL Aggiungi elemento]** per aggiungere un’altra scelta di valutazione.

Sotto la **[!UICONTROL Valutazioni richieste]** , reinserire elementi dall’elenco di **[!UICONTROL Valutazioni consentite]** che devono essere valutate. Se un elemento è specificato solo nella scheda Valutazioni consentite, può essere lasciato senza contrassegno quando viene inviato dal membro.

Sul sito web, le valutazioni richieste sono contrassegnate da un asterisco. Se un elemento è obbligatorio e lasciato senza contrassegno, viene visualizzato un messaggio al membro e l&#39;invio viene negato fino a quando non vengono contrassegnate tutte le valutazioni richieste.

![classificazione obbligatoria](assets/configure-review2.png)

* **[!UICONTROL Classificazioni richieste]**

   Un sottoinsieme di rating consentiti, che indica quali rating sono richiesti.

   Utilizzare i pulsanti freccia su, freccia giù ed Elimina per modificare le selezioni visibili.

   Fai clic su **[!UICONTROL Aggiungi elemento]** per aggiungere un’altra scelta di risposta.

>[!NOTE]
>
>Se un articolo è inserito nella sezione **[!UICONTROL Valutazioni richieste]** scheda non specificata nel **[!UICONTROL Valutazioni consentite]** quindi non è incluso negli elementi da valutare.

Sotto la **[!UICONTROL Recensioni]** scheda , specifica come vengono gestite le revisioni.

![recensioni](assets/configure-review3.png)

* **[!UICONTROL Consenti risposte]**

   Se questa opzione è selezionata, consentire le risposte alle revisioni. Il valore predefinito è deselezionato.

* **[!UICONTROL Chiuso]**

   Se questa opzione è selezionata, la revisione è chiusa a nuove recensioni e risposte. Il valore predefinito è deselezionato.

* **[!UICONTROL Consenti caricamenti file]**

   Se questa opzione è selezionata, consenti il caricamento di allegati di file per la revisione. Il valore predefinito è deselezionato.

* **Dimensione file massima**

   Pertinente solo se **[!UICONTROL Consenti caricamenti file]** è controllata. Questo campo limita le dimensioni (in byte) di un file caricato. Il valore predefinito è 10 MB.

* **[!UICONTROL Lunghezza massima messaggio]**

   Numero massimo di caratteri che possono essere immessi nella casella di testo. Il valore predefinito è 4096 caratteri.

* **[!UICONTROL Tipi di file consentiti]**

   Pertinente solo se **[!UICONTROL Consenti caricamenti file]** è controllata. Elenco di estensioni di file separate da virgola con il separatore &quot;punto&quot;. Ad esempio: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se sono specificati tipi di file, quelli non specificati non saranno consentiti. Il valore predefinito non è specificato in modo che tutti i tipi di file siano consentiti.

* **[!UICONTROL Editor Rich Text]**

   Se questa opzione è selezionata, i post possono essere inseriti con markup. Il valore predefinito è deselezionato.

* **[!UICONTROL Consenti votazione]**

   Se questa opzione è selezionata, includi la funzione di voto per un argomento. Il valore predefinito è deselezionato.

Sotto la **[!UICONTROL Moderazione utente]** scheda , specifica come vengono gestite le revisioni pubblicate. Per ulteriori informazioni, consulta [Moderazione dei contenuti generati dagli utenti](moderate-ugc.md).

![moderazione dell&#39;utente](assets/configure-review4.png)

* **[!UICONTROL Premoderazione]**

   Se questa opzione è selezionata, le revisioni devono essere approvate prima che vengano visualizzate su un sito di pubblicazione. Il valore predefinito è deselezionato.

* **[!UICONTROL Elimina recensioni]**

   Se questa opzione è selezionata, al membro che ha pubblicato la revisione viene offerta la possibilità di eliminarla. Il valore predefinito è deselezionato.

* **[!UICONTROL Rifiuta recensioni]**

   Se questa opzione è selezionata, consentire ai moderatori di negare le revisioni. Il valore predefinito è deselezionato.

* **[!UICONTROL Chiudi/Riapri recensioni]**

   Se questa opzione è selezionata, consenti ai moderatori di chiudere e riaprire le revisioni. Il valore predefinito è deselezionato.

* **[!UICONTROL Segnala recensioni]**

   Se questa opzione è selezionata, consenti ai membri di contrassegnare le revisioni come inadeguate. Il valore predefinito è deselezionato.

* **[!UICONTROL Elenco di motivi per segnalazione]**

   Se questa opzione è selezionata, consentire ai membri di scegliere, da un elenco a discesa, il motivo per cui contrassegnano una revisione come inappropriato. Il valore predefinito è deselezionato.

* **[!UICONTROL Motivo per segnalazione personalizzato]**

   Se questa opzione è selezionata, consenti ai membri di inserire il proprio motivo per contrassegnare una revisione come inappropriata. Il valore predefinito è deselezionato.

* **[!UICONTROL Soglia moderazione]**

   Immettere il numero di volte in cui una revisione deve essere contrassegnata dai membri prima che i moderatori siano informati. Il valore predefinito è una tantum (1).

* **[!UICONTROL Limite segnalazione]**

   Immetti il numero di volte in cui una revisione deve essere contrassegnata prima che sia nascosta dalla visualizzazione pubblica. Questo numero deve essere maggiore o uguale a **[!UICONTROL Soglia moderazione]**. Il valore predefinito è 5.

### Aggiunta di un riepilogo della revisione (visualizzazione) a una pagina {#adding-a-review-summary-display-to-a-page}

Per aggiungere una `Reviews Summary (Display)` in una pagina in modalità di authoring, individua il componente

* `Communities / Reviews Summary (Display)`

e trascinarlo nella posizione in una pagina in cui deve essere visualizzato un riepilogo di una revisione attiva o chiusa.

Per le informazioni necessarie, visita [Nozioni di base sui componenti di Communities](basics.md).

Quando il [librerie lato client richieste](reviews-basics.md#essentials-for-client-side) sono inclusi, è così che `Reviews Summary (Display)`apparirà .

![riepilogo delle revisioni](assets/configure-review5.png)

>[!NOTE]
>
>La &quot;media&quot; riflette i voti per il primo elemento elencato nelle schede Valutazioni consentite della revisione che viene riepilogata.

### Riepilogo della configurazione delle revisioni (visualizzazione) {#configuring-reviews-summary-display}

Seleziona il `Reviews Summary (Display)` per accedere e selezionare il `Configure` che apre la finestra di dialogo di modifica.

![configurare](assets/configure-new.png)

Sotto la **[!UICONTROL Riepilogo]** scheda

![riepilogo delle revisioni](assets/configure-review6.png)

* `Review Path`

   entra o sfoglia fino all’istanza inserita del `reviews`componente per riepilogare, ad esempio, se aggiunto alla pagina Web del [Sito Geometrixx Engage,](getting-started.md) il percorso sarebbe:

   `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

   Se questa opzione è selezionata, includi la visualizzazione di un grafico a barre che indica il numero di stelle di valutazione presenti nelle revisioni da riepilogare. Il valore predefinito è deselezionato.

### Modifica a un tipo di revisione personalizzato {#changing-to-a-custom-review-type}

Il componente Revisioni utilizza il sistema di commenti.

Modificando il tipo di risorsa commento, il sistema di commento non genererà più un&#39;istanza di un commento utilizzando il valore predefinito, ma piuttosto un&#39;istanza personalizzata (estesa) dagli sviluppatori.

Una volta noti i tipi di risorse personalizzati, immetti [Modalità Progettazione](../../help/sites-authoring/default-components-designmode.md) e fai doppio clic sul `Comments` per aprire una finestra di dialogo con una scheda aggiuntiva.

Sotto la **[!UICONTROL Tipi di risorse]** specifica il resourceType personalizzato per le nuove istanze del `Comments or Voting` componenti:

![voto ai commenti](assets/configure-review7.png)

* **[!UICONTROL Tipo risorsa commento]**

   Passa al resourceType di un esteso `comment`componente (singolo commento) in /apps. Esempio: `/apps/social/commons/components/hbs/comments/comment`.

   Questa risorsa identificherà il resourceType dell&#39;UGC creato quando un visitatore pubblica un commento.

* **[!UICONTROL Tipo di risorsa per votazione]**

   Passa al resourceType di un esteso `voting`in /apps. Esempio: `/apps/social/components/hbs/voting`.

   Questa risorsa identificherà il tipo di risorsa dell’UGC creato quando un visitatore pubblica un voto.

* **[!UICONTROL Tipo risorsa sistema di commenti]**

   Passa al resourceType di un esteso `comments`componente (sistema di commenti) in /apps. Lascia vuoto a meno che il modello di pagina [include dinamicamente](scf.md#add-or-include-a-communities-component) il sistema di commenti nello script sottostante anziché essere aggiunto alla pagina come risorsa (nodo di commenti). Per saperne di più, leggi [{{include}} aiutante](handlebars-helpers.md#include).

## Esperienza dei visitatori del sito {#site-visitor-experience}

### Moderatori e amministratori {#moderators-and-administrators}

Quando l’utente connesso dispone di privilegi di moderatore o amministratore, può eseguire le attività di moderazione consentite dalla configurazione del componente, indipendentemente da chi ha creato la revisione.

### Membri {#members}

Quando il visitatore del sito effettua l’accesso, a seconda della configurazione, può:

* Pubblica una nuova recensione
* Modifica la propria revisione
* Elimina la propria revisione
* Contrassegna i commenti di revisione degli altri

È consentita una sola classificazione per membro. Il membro può modificare il proprio rating in qualsiasi momento.

### Anonimo {#anonymous}

I visitatori del sito che non hanno effettuato l&#39;accesso possono solo leggere le revisioni pubblicate, tradurle se supportate, ma non possono aggiungere una valutazione o una revisione, né contrassegnare i commenti di revisione di altri.

## Informazioni aggiuntive {#additional-information}

Per ulteriori informazioni, consulta [Rivedi le nozioni di base](reviews-basics.md) per sviluppatori.

Per la moderazione dei commenti pubblicati, vedere [Moderazione dei contenuti generati dagli utenti](moderate-ugc.md).

Per la traduzione dei commenti pubblicati, consultare [Traduzione di contenuti generati dagli utenti](translate-ugc.md).
