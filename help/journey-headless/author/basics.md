---
title: Scopri le nozioni di base sull’authoring
description: Scopri cos’è e come funziona l’authoring per i CMS headless utilizzando frammenti di contenuto.
exl-id: 125c4d0b-1572-4dba-823d-cdef2778f275
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 75%

---

# Nozioni di base sull’authoring per headless con AEM {#author-headless-basics}

## Percorso affrontato finora {#story-so-far}

All’inizio del [Percorso di authoring dei contenuti headless in AEM](overview.md), nell’[Introduzione](introduction.md) sono stati trattati i concetti e la terminologia di base relativi all’authoring per headless.

Questo articolo si basa su questi elementi per comprendere come creare contenuti personalizzati per il progetto headless AEM.

## Obiettivo {#objective}

* **Pubblico**: principiante
* **Obiettivo**: scopri le nozioni di base sull’authoring di CMS headless:
   * introduzione all’authoring con AEMaaCS
   * Introduzione ai frammenti di contenuto

## Operazioni di base {#basic-handling}

Prima di iniziare a gestire i frammenti di contenuto, ecco un’introduzione (molto) rapida all’utilizzo di AEM...ma niente sostituisce l’esperienza di accesso e di utilizzo del sistema.

### Creazione e pubblicazione {#author-preview-publish}

Un’installazione di AEM è in genere costituita da almeno due ambienti:

* Autore
* Pubblicazione

Accedi e utilizza l’ambiente di authoring per generare i contenuti. Quando è tutto pronto, pubblica il contenuto in modo che diventi disponibile. Per gli headless sarà disponibile in altre applicazioni, per le pagine web sarà disponibile ai lettori sul web.

Per ulteriori dettagli, consulta i concetti di authoring.

### Accesso {#signing-in}

Come per la maggior parte dei sistemi, è necessario effettuare l&#39;accesso. In qualità di autore, riceverai:

* Nome utente (account)
* Password
* Collegamento per accedere alla schermata di accesso

Il tuo account sarà stato configurato con tutti i privilegi necessari. In caso di problemi, Adobe consiglia di contattare il team di supporto interno per il progetto.

### Navigazione {#navigation}

La prima volta che esegui l’accesso a una piccola esercitazione online, verranno evidenziate alcune delle funzioni principali dell’interfaccia utente.

È quindi possibile utilizzare il pannello di navigazione per accedere alle aree chiave di AEM. Per i frammenti di contenuto utilizzerai **Console risorse**.

Per aprire il pannello di navigazione, seleziona l’icona Adobe in alto a sinistra, seguita dall’icona della bussola piccola:

![Pannello di navigazione](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)

>[!NOTE]
>Sebbene i frammenti di contenuto siano una funzione dell’AEM **Sites**, si trovano in **Risorse** console. Questo è un dettaglio tecnico che non dovrebbe influenzare l’utente, ma potrebbe essere utile da sapere.

All’interno della console puoi selezionare le cartelle per passare al frammento di contenuto oppure le breadcrumb (nell’intestazione) per tornare alla struttura.

![Breadcrumb](/help/journey-headless/author/assets/headless-journey-author-navigation-02.png)

### Azioni, selezione, visualizzazione {#actions-selecting-viewing}

Il **Risorse** la console ha dedicato **Barre degli strumenti delle azioni**, e **Azioni rapide** che puoi utilizzare dopo aver selezionato una risorsa (ad esempio, una cartella o un frammento di contenuto).

Le Azioni rapide sono disponibili per una singola risorsa, vedi **Basilea** nell’esempio seguente:

![Azioni rapide](/help/journey-headless/author/assets/headless-journey-author-navigation-05.png)

La barra degli strumenti Azioni consente di accedere a tutte le azioni applicabili allo scenario corrente. Le azioni disponibili possono variare, ad esempio a seconda della posizione o se sono state selezionate più risorse:

![Barra delle azioni](/help/journey-headless/author/assets/headless-journey-author-navigation-06.png)

Puoi selezionare il formato di visualizzazione delle risorse con il Selettore di visualizzazione:

![Selettore vista](/help/journey-headless/author/assets/headless-journey-author-navigation-03.png)

Puoi visualizzare ulteriori informazioni sugli elementi utilizzando il Selettore della barra. Ciò consente anche di accedere ad azioni aggiuntive.

![Barra a sinistra](/help/journey-headless/author/assets/headless-journey-author-navigation-04.png)

## Authoring dei frammenti di contenuto {#authoring-content-fragments}

Questa è stata una rapida introduzione all’interfaccia utente AEM, ma dovresti aver avuto l’occasione di provarla. Ora passiamo a quello che ti interessa di più: frammenti di contenuto per headless.

Dovremo passare dall’inizio alla fine delle operazioni, ma l’istanza potrebbe avere già cartelle e/o frammenti creati, che potrebbero trovarsi in posizioni diverse. I principi sono gli stessi.

### Organizzazione e navigazione {#organizing-and-navigating}

A meno che non siano disponibili pochissimi frammenti di contenuto, è consigliabile organizzarli in modo da poterli trovare nuovamente (insieme ad altri).

#### Creazione di una cartella {#creating-folder}

Per farlo, crea una serie di cartelle in **File** della console Assets. Seleziona l’opzione **Crea** (in alto a destra), seguita da **Cartella**:

![Opzione Crea cartella](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

Viene visualizzata una finestra di dialogo in cui puoi inserire i dettagli, quindi confermare con **Crea**:

![Finestra di dialogo Crea cartella](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### Utilizzo di percorsi e tag per limitare i modelli per frammenti di contenuto disponibili nella cartella {#tags-paths-for-models-in-folder}

Questa sezione è leggermente più avanzata. Non ne hai veramente bisogno se stai solo iniziando e provando le cose, ma è più utile quando hai molti frammenti. Quindi è bene conoscerla, anche se non la stai ancora usando.

L’architect di contenuti avrà creato tutti i modelli di frammento di contenuto necessari per il progetto corrente e forse anche altri progetti. Per semplificare le cose a te stesso e agli altri autori, puoi limitare l’elenco dei modelli disponibili per una cartella specifica.

Dopo aver creato la tua cartella è possibile aprire la cartella **Proprietà**. Qui ci sono varie schede con informazioni e dettagli di configurazione sulla cartella. In particolare per i frammenti di contenuto, puoi utilizzare la scheda **Criteri** per definire percorsi e/o tag specifici per questa cartella. Questo limita i modelli per frammenti di contenuto disponibili per l’utilizzo nella cartella, poiché i modelli per frammenti di contenuto devono soddisfare questi requisiti prima di poter essere utilizzati per generare frammenti in questa cartella.

![Crea proprietà cartella - Criteri](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>Per ulteriori informazioni, consulta Modelli per frammenti di contenuto - Consentire modelli per frammenti di contenuto nella cartella delle risorse.

Puoi quindi navigare tra queste cartelle per creare e modificare i frammenti di contenuto.

#### In caso - Configurazione cartella Cloud Services {#cloud-services-folder}

In caso...

Probabilmente ti verrà offerta una cartella iniziale in cui puoi creare le tue cartelle. Come alcuni dettagli di configurazione devono essere applicati alla cartella principale (in genere da uno sviluppatore o da un amministratore di sistema). Probabilmente non ti interessa, ma se necessario puoi controllare il **Configurazione** nel **Cloud Service** della cartella **Proprietà**:

![Crea proprietà cartella - Configurazione](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>Per ulteriori informazioni, consulta Applicare la configurazione alla cartella Risorse.

### Creazione di un frammento di contenuto {#creating-fragment}

La creazione di un frammento di contenuto è molto simile: puoi semplicemente utilizzare **Frammento di contenuto** invece:

![Opzione Crea frammento di contenuto](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

Questa volta viene aperta una procedura guidata. Il primo passaggio consiste nel selezionare il modello per frammenti di contenuto su cui basare il frammento:

![Crea frammento di contenuto - seleziona modello](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

Dopo aver continuato con **Successivo** è possibile specificare i dettagli (**Base** e **Avanzate**) per il frammento:

![Crea frammento di contenuto: specificare il nome](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

Conferma con **Crea** e puoi quindi **Apri** frammento nell’editor.

### Modifica di un frammento {#editing-fragment}

Puoi aprire un frammento immediatamente dopo averlo creato o selezionandolo dalla console Assets.

Quando l’editor si apre per la prima volta, vedrai:

* Un elenco di icone a sinistra permette di accedere a varie aree di funzionalità. L’editor si apre nella scheda **Variazioni**, in questo punto avviene la maggior parte delle modifiche. Potresti anche essere interessato alle schede **Annotazioni** e **Metadati**.

* Intestazione con informazioni sul frammento e accesso a varie azioni.

* L’area di modifica principale dipende dal modello utilizzato per creare il frammento.

Come esempi:

* Frammento che richiede solo più informazioni, alcune con un tipo specifico. Come scoprirai andando avanti nel tuo percorso, i riferimenti sono fondamentali per i contenuti headless.

  ![Editor frammento di contenuto - Frammento personale](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* Frammento che consente di scrivere una lunga sezione di testo. Qui sono disponibili opzioni aggiuntive per la gestione e la formattazione del testo. Puoi anche aprire i singoli campi di testo in un editor a schermo intero (utilizzando l’icona a forma di piccolo schermo a destra)

  ![Editor frammento di contenuto - Alaska Spirits](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>Per aiutare gli autori a completare alcuni campi correttamente, potrebbe essere necessaria una documentazione specifica per il progetto.
>
>Consulta Modelli per frammenti di contenuto - Tipi di dati e proprietà per dettagli generici.

Conferma gli aggiornamenti con **Salva** o **Salva e chiudi**.

>[!NOTE]
>
>Per ulteriori informazioni, consulta Varianti - Authoring di frammenti di contenuto.

#### Quello di cui (probabilmente) non devi preoccuparti {#what-you-probably-do-not-need-to-worry-about}

OK, questa potrebbe sembrare una sezione leggermente ambigua, ma una volta aperto l’Editor frammento di contenuto e iniziato ad esplorarlo, vedrai diverse opzioni che (probabilmente) non si adattano al tuo percorso headless come Autore di contenuto. Questo è solo un rapido resoconto di ciò che dovresti essere in grado di ignorare nel contesto headless:

* **Modelli per frammenti di contenuto**

  Il nome del modello di frammento di contenuto verrà visualizzato nella parte superiore dell’editor, direttamente sotto il nome del frammento. Questo è anche un collegamento che ti porta all’editor modelli.
I modelli per frammenti di contenuto sono di fatto vitali per i frammenti di contenuto quando definiscono la struttura utilizzata. Tuttavia, la creazione e la modifica di tali elementi è (in genere) responsabilità di un’altra persona, l’architect di contenuti.

  >[!NOTE]
  >
  >Per ulteriori informazioni, consulta il Percorso Architect di contenuti AEM headless.

* **Contenuto associato**

  Questo è abbastanza ovvio in quanto si tratta di una scheda nell’editor.

  I frammenti di contenuto sono disponibili in AEM in diverse versioni. Originariamente erano disponibili per l’uso “tradizionale” durante l’authoring delle pagine....e sono ancora utilizzati in questo contesto. Questo può comportare l’associazione di risorse (ad esempio immagini) che, pur non essendo incorporate nel frammento, devono essere disponibili per l’autore durante l’authoring di una pagina.

* **Anteprima**

  Questa è un’altra scheda nell’editor e fornisce una vista tecnica, destinata principalmente agli sviluppatori.

* **Aggiorna i riferimenti di pagina**

  Questa azione è disponibile nel menu a discesa **...** (puntini di sospensione). Non è interessante per gli autori headless in quanto si riferisce all’authoring delle pagine.

### Pubblicazione {#publishing}

<!-- needs more details -->

Una volta completato il frammento, puoi **Pubblicare** in modo che sia disponibile per le applicazioni headless.

Le azioni di pubblicazione sono disponibili nell’editor (o dalla barra degli strumenti del **Risorse** console):

![Editor frammento di contenuto - Frammento personale](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

## Passaggio successivo {#whats-next}

Ora che hai imparato le nozioni di base, il passo successivo è [Scopri come utilizzare i riferimenti](references.md). Questo introduce e illustra i vari riferimenti disponibili e come creare livelli di struttura con i Riferimenti ai frammenti, una parte chiave dell’authoring per gli oggetti headless.

## Risorse aggiuntive {#additional-resources}

* [Concetti relativi all’authoring](/help/sites-authoring/author.md)

* [Operazioni di base](/help/sites-authoring/basic-handling.md) - questa pagina si basa principalmente sulla console **Sites**, ma molte delle funzioni sono anche rilevanti per l’authoring **Frammenti di contenuto** nella console **Risorse**.

   * [Pannello di navigazione](/help/sites-authoring/basic-handling.md#navigation-panel)

   * [Intestazione](/help/sites-authoring/basic-handling.md#the-header)

   * [Barra degli strumenti delle azioni](/help/sites-authoring/basic-handling.md#actions-toolbar)

   * [Azioni rapide](/help/sites-authoring/basic-handling.md#quick-actions)

   * [Visualizzazione e selezione delle risorse](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)

   * [Selettore della barra](/help/sites-authoring/basic-handling.md#rail-selector)

* [Utilizzo di frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)

   * [Gestione dei frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md)

      * [Applica la configurazione alla cartella Risorse](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [Creazione di un frammento di contenuto](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)

   * [Varianti - Authoring di frammenti di contenuto](/help/assets/content-fragments/content-fragments-variations.md)

   * [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)

      * [Modelli per frammenti di contenuto - Tipi di dati](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [Modelli per frammenti di contenuto - Proprietà](/help/assets/content-fragments/content-fragments-models.md#properties)

      * [Modelli per frammenti di contenuto - Consentire modelli per frammenti di contenuto nella cartella delle risorse](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

* Guide introduttive
   * [Guida rapida alla creazione di una cartella di risorse headless](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [Percorso Architect di contenuti AEM headless](/help/journey-headless/architect/overview.md)

* [Percorso di traduzione headless di AEM](/help/journey-headless/translation/overview.md)
