---
title: Modifica del contenuto di una pagina
seo-title: Editing Page Content
description: Una volta creata la pagina, è possibile modificarla per aggiornarne i contenuti
seo-description: Once your page is created you can edit the content to make the updates you require
uuid: 5b4f0a8f-5196-42ea-8413-203783a0b77b
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: f92ed674-5865-4a53-8c3a-369536861f14
docset: aem65
exl-id: d5cf4478-51e4-4ca8-b3f8-6d7caed7d515
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3045'
ht-degree: 93%

---

# Modifica del contenuto di una pagina{#editing-page-content}

Una volta creata la pagina (nuova o come parte di un lancio o una live copy) è possibile aggiornarla modificandone i contenuti.

Per aggiungere i contenuti si trascinano sulla pagina specifici [componenti](/help/sites-authoring/default-components-console.md), in base al tipo di contenuto, che possono quindi essere modificati, spostati o eliminati.

>[!NOTE]
>
>Il tuo account deve disporre dei [diritti di accesso](/help/sites-administering/security.md) e delle [autorizzazioni](/help/sites-administering/security.md#permissions) adeguate per intervenire sulle pagine.
>
>Nell’eventualità di problemi, rivolgiti al tuo amministratore di sistema.

>[!NOTE]
>
>Se la pagina e/o il modello sono stati impostati in modo appropriato, è possibile utilizzare il [layout dinamico](/help/sites-authoring/responsive-layout.md) durante la modifica.

>[!NOTE]
>
>In modalità **Modifica**, i collegamenti presenti nel contenuto sono visibili, ma **non accessibili**. Utilizza la modalità [Anteprima](#previewingpagestouchoptimizedui) se desideri navigare utilizzando i collegamenti presenti nel tuo contenuto.

## Barra degli strumenti della pagina {#page-toolbar}

Dalla barra degli strumenti della pagina è possibile accedere alle funzionalità appropriate, a seconda della configurazione della pagina.

![screen_shot_2018-03-22at111338](assets/screen_shot_2018-03-22at111338.png)

La barra degli strumenti offre l&#39;accesso a numerose opzioni. A seconda del contesto e della configurazione corrente, alcune opzioni potrebbero non essere disponibili.

* **Attiva/Disattiva pannello laterale**

   Apre/chiude il pannello laterale che contiene il [Browser delle risorse](/help/sites-authoring/author-environment-tools.md#assets-browser), il [Browser dei componenti](/help/sites-authoring/author-environment-tools.md#components-browser) e la [struttura contenuto](/help/sites-authoring/author-environment-tools.md#content-tree).

   ![](do-not-localize/screen_shot_2018-03-22at111425.png)

* **Informazioni sulle pagine**

   Consente di accedere al menu [Informazioni pagina](/help/sites-authoring/author-environment-tools.md#page-information), che contiene i dettagli della pagina e le azioni che possono essere eseguite su di essa. Per esempio: visualizzare e modificare le informazioni sulla pagina, visualizzare le proprietà della pagina, pubblicare la pagina o annullare la pubblicazione.

   ![](do-not-localize/screen_shot_2018-03-22at111437.png)

* **Emulatore**

   Attiva o disattiva la [barra degli strumenti dell’emulatore](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate), che permette di simulare l’aspetto che avrà la pagina su un altro dispositivo. Questa barra è automaticamente attivata in modalità di layout.

   ![](do-not-localize/screen_shot_2018-03-22at111442.png)

* **ContextHub**

   Consente di aprire il [context hub](/help/sites-authoring/ch-previewing.md). Disponibile solo in modalità Anteprima.

   ![screen_shot_2018-03-22at111543](assets/screen_shot_2018-03-22at111543.png)

* **Titolo pagina**

   Questa sezione è solo a scopo informativo.

   ![screen_shot_2018-03-22at111554](assets/screen_shot_2018-03-22at111554.png)

* **Selettore modalità**

   Mostra la [modalità](/help/sites-authoring/author-environment-tools.md#page-modes) corrente e consente di selezionarne un’altra come, come per esempio Modifica, Layout, Timewarp o Targeting.

   ![chlimage_1-120](assets/chlimage_1-120.png)

* **Anteprima**

   Abilita la [modalità Anteprima](/help/sites-authoring/editing-content.md#preview-mode). La pagina viene visualizzata così come apparirà una volta pubblicata.

   ![chlimage_1-121](assets/chlimage_1-121.png)

* **Annotazioni**

   Consente di aggiungere [annotazioni](/help/sites-authoring/annotations.md) alla pagina durante la revisione. Dopo la prima annotazione, l’icona viene sostituita da un numero che indica quante annotazioni sono presenti sulla pagina.

   ![](do-not-localize/screen_shot_2018-03-22at111638.png)

### Notifica di stato {#status-notification}

Se una pagina fa parte di uno o più [flussi di lavoro](/help/sites-authoring/workflows.md), queste informazioni vengono visualizzate in una barra di notifica nella parte superiore dello schermo durante la modifica della pagina.

![screen_shot_2018-03-22at111739](assets/screen_shot_2018-03-22at111739.png)

>[!NOTE]
>
>La barra di stato è visibile solo per gli account utente che dispongono dei diritti appropriati.

La notifica riporta il flusso di lavoro in esecuzione sulla pagina. Se l’utente è coinvolto nella fase attuale del flusso di lavoro, sono anche disponibili opzioni per [modificare lo stato del flusso di lavoro](/help/sites-authoring/workflows-participating.md) e ottenere ulteriori informazioni sul flusso di lavoro. Per esempio:

* **Completa** - Apre la **Elemento di lavoro completo** dialogo

* **Delega** - Apre la **Elemento di lavoro completo** dialogo

* **Visualizza dettagli**: apre la finestra **Dettagli** del flusso di lavoro

Il completamento e la delega delle fasi del flusso di lavoro a partire dalla barra delle notifiche funzionano in modo analogo alla [partecipazione ai flussi di lavoro](/help/sites-authoring/workflows-participating.md) a partire dalla casella in entrata delle Notifiche.

Se la pagina è soggetta a più flussi di lavoro, il numero dei flussi di lavoro viene visualizzato all’estremità destra della notifica, insieme ai pulsanti freccia che consentono di scorrere i flussi di lavoro.

![chlimage_1-122](assets/chlimage_1-122.png)

## Segnaposto Componente {#component-placeholder}

Il segnaposto del componente è un indicatore che mostra dove verrà posizionato il componente al momento del rilascio, sopra il componente sul quale si trova il puntatore del mouse in quel momento.

* Quando si aggiunge un nuovo componente alla pagina (trascinandolo dal browser Componenti):

   ![screen_shot_2018-03-22at111928](assets/screen_shot_2018-03-22at111928.png)

* Quando si sposta un componente esistente:

   ![screen_shot_2018-03-22at112445](assets/screen_shot_2018-03-22at112445.png)

## Inserimento di un componente {#inserting-a-component}

### Inserire un componente dal Browser Componenti {#inserting-a-component-from-the-components-browser}

È possibile aggiungere un nuovo componente utilizzando il [browser componenti](/help/sites-authoring/author-environment-tools.md#components-browser). Il [segnaposto componente](#component-placeholder) mostra dove sarà posizionato il componente:

1. Assicurati che la pagina sia in [**modalità Modifica**.](/help/sites-authoring/author-environment-tools.md#page-modes)
1. Apri il [browser Componenti](/help/sites-authoring/author-environment-tools.md#components-browser).
1. Trascina il componente di cui hai bisogno nella [posizione desiderata](#component-placeholder).

1. [Modifica](#editmovecopypastedelete) il componente.

>[!NOTE]
>
>Su un dispositivo mobile, il browser Componenti occuperà l’intero schermo. Quando si inizia a trascinare un componente, il browser si chiude per mostrare nuovamente la pagina, in modo che il componente possa essere posizionato facilmente.

### Inserimento di un Componente dal Sistema Paragrafo   {#inserting-a-component-from-the-paragraph-system}

È possibile aggiungere un nuovo componente utilizzando la casella **Trascina qui i componenti** del sistema paragrafo:

1. Assicurati che la pagina sia in [**modalità Modifica**.](/help/sites-authoring/author-environment-tools.md#page-modes)
1. Esistono due modi per selezionare e aggiungere un nuovo componente dal sistema paragrafo:

   * Seleziona l’opzione **Inserisci componente** (+) nella barra degli strumenti di un componente esistente oppure nella casella **Trascina qui i componenti**.

   ![screen_shot_2018-03-22at112536](assets/screen_shot_2018-03-22at112536.png)

   * Se utilizzi un dispositivo desktop, puoi fare doppio clic sulla casella **Trascina qui i componenti**.

   Viene visualizzata la finestra di dialogo **Inserisci nuovo componente**, che consente di selezionare il componente richiesto:

   ![screen_shot_2018-03-22at112650](assets/screen_shot_2018-03-22at112650.png)

1. Il componente selezionato verrà aggiunto in fondo alla pagina. [Modifica](#editmovecopypastedelete) il componente come preferisci.

### Inserimento di un componente utilizzando il browser Risorse   {#inserting-a-component-using-the-assets-browser}

È possibile aggiungere un nuovo componente alla pagina anche trascinando una risorsa dal [browser Risorse](/help/sites-authoring/author-environment-tools.md#assets-browser). Questo determina la creazione automatica di un nuovo componente del tipo appropriato (e che include la risorsa).

Questo vale per i seguenti tipi di risorse (alcune dipenderanno dal sistema della pagina o del paragrafo):

<table>
 <tbody>
  <tr>
   <th><strong>Tipo risorsa</strong></th>
   <th><strong>Tipo componente risultante</strong></th>
  </tr>
  <tr>
   <td>Immagine</td>
   <td>Immagine</td>
  </tr>
  <tr>
   <td>Documento</td>
   <td>Scarica</td>
  </tr>
  <tr>
   <td>Prodotto</td>
   <td>Prodotto</td>
  </tr>
  <tr>
   <td>Video</td>
   <td>Flash</td>
  </tr>
  <tr>
   <td>Frammenti di contenuto</td>
   <td>Frammenti di contenuto<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Puoi configurare questo comportamento per l’installazione in uso. Per ulteriori dettagli, vedere la sezione su come [Configurare un sistema di paragrafi in modo che il trascinamento di una risorsa crei uno specifico componente](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance).

Per creare un componente trascinando uno dei tipi di risorsa indicati sopra:

1. Assicurati che la pagina sia in [**modalità Modifica**.](/help/sites-authoring/author-environment-tools.md#page-modes)
1. Apri il [browser Risorse](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. Trascina la risorsa richiesta nella posizione desiderata. Il [segnaposto componente](#component-placeholder) indica dove sarà posizionato il componente.

   In tale posizione viene creato un componente adatto al tipo di risorsa, che include la risorsa selezionata.

1. Se necessario, [Modifica](#editmovecopypastedelete) il componente.

>[!NOTE]
>
>Su un dispositivo mobile, il browser Risorse occuperà l’intero schermo. Quando inizi a trascinare una risorsa, il browser si chiude per mostrare nuovamente la pagina e permetterti di posizionare la risorsa.

Se sfogliando le risorse disponibili scopri che è necessario eseguire una rapida modifica a una risorsa, puoi avviare l’[editor delle risorse](/help/assets/manage-assets.md) direttamente dal browser, facendo clic sull’icona di modifica accanto al nome della risorsa.

![screen_shot_2018-03-22at112735](assets/screen_shot_2018-03-22at112735.png)

## Modificare/configurare/copiare/tagliare/eliminare/incollare {#edit-configure-copy-cut-delete-paste}

Selezionando un componente si aprirà la barra degli strumenti, che consente di accedere alle azioni disponibili per tale componente.

Le azioni disponibili dipendono dal contesto; in questa sezione ne vengono descritte solo alcune.

![screen_shot_2018-03-22at112909](assets/screen_shot_2018-03-22at112909.png)

* **Modifica**

   [In base al tipo di componente,](/help/sites-authoring/default-components.md) questo comando consente di [modificare il contenuto del componente](#edit-content). Spesso è disponibile una barra degli strumenti.

   ![](do-not-localize/screen_shot_2018-03-22at112936.png)

* **Configura**

   [In base al tipo di componente,](/help/sites-authoring/default-components.md) questo comando consente di modificare e configurare le proprietà del componente. In genere presenta una finestra di dialogo.

   ![](do-not-localize/screen_shot_2018-03-22at112955.png)

* **Copia**

   Questo comando consente di copiare il componente negli Appunti. Dopo l’operazione Incolla, il componente originale non viene eliminato.

   ![](do-not-localize/screen_shot_2018-03-22at113000.png)

* **Taglia**

   Questo comando consente di copiare il componente negli Appunti. Dopo l’operazione Incolla, il componente originale viene eliminato.

   ![screen_shot_2018-03-22at113007](assets/screen_shot_2018-03-22at113007.png)

* **Eliminare**

   Questo comando elimina il componente dalla pagina, previa conferma.

   ![](do-not-localize/screen_shot_2018-03-22at113012.png)

* **Inserisci componente**

   Con questo comando si apre la finestra di dialogo che consente di [aggiungere un nuovo componente](/help/sites-authoring/editing-content.md#inserting-a-component-from-the-paragraph-system).

   ![](do-not-localize/screen_shot_2018-03-22at113017.png)

* **Incolla**

   Questo comando consente di incollare il componente dagli Appunti alla pagina. Il componente originale viene eliminato o meno a seconda dell’opzione precedentemente utilizzata (rispettivamente Taglia o Copia).

   * È possibile incollare i componenti sulla stessa pagina o su una pagina diversa.
   * L’elemento viene incollato sopra quello nella cui posizione di seleziona l’azione Incolla.
   * L’azione Incolla è disponibile solo se è presente contenuto negli Appunti.

   ![screen_shot_2018-03-22at113553](assets/screen_shot_2018-03-22at113553.png)

   >[!NOTE]
   >
   >Se incolli in un’altra pagina che era già aperta prima dell’operazione taglia/copia, per visualizzare il contenuto incollato devi aggiornare la pagina.

* **Gruppo**

   Questa opzione consente di selezionare più componenti contemporaneamente. La stessa operazione è possibile su un dispositivo desktop tramite **Control+clic** o **Comando+clic**.

   ![](do-not-localize/screen_shot_2018-03-22at113240.png)

* **Elemento padre**

   Consente di selezionare l’elemento padre del componente selezionato.

   ![screen_shot_2018-03-22at113028](assets/screen_shot_2018-03-22at113028.png)

* **Layout**

   Questa opzione consente di modificare il [layout](/help/sites-authoring/editing-content.md#edit-component-layout) del componente selezionato. Ciò vale solo per il componente selezionato e non attiva la [Modalità di layout](/help/sites-authoring/author-environment-tools.md#page-modes) per l’intera pagina.

   ![](do-not-localize/screen_shot_2018-03-22at113044.png)

* **Converti in variante di frammento di esperienza**

   Consente di creare un nuovo [Frammento esperienza](/help/sites-authoring/experience-fragments.md) dal componente selezionato o di aggiungerlo a un frammento di esperienza esistente.

   ![](do-not-localize/screen_shot_2018-03-22at113033.png)

## Modifica (Contenuto) {#edit-content}

Esistono due metodi per aggiungere e/o modificare contenuti nei componenti:

* Apri la [finestra di dialogo del componente per la modifica](#component-edit-dialog).
* Per aggiungere direttamente contenuti [trascina una risorsa](#draganddropintocomponent) dal browser risorse.

### Finestra di dialogo di modifica del componente   {#component-edit-dialog}

Puoi aprire un componente per modificarne il contenuto utilizzando l’icona [Modifica (matita) nella barra degli strumenti del componente](#edit-configure-copy-cut-delete-paste).

Le opzioni di modifica effettive dipendono dal componente. Per alcuni componenti [tutte le azioni sono disponibili solo in modalità a schermo intero](#edit-content-full-screen-mode). Esempio:

* [Componente testo](/help/sites-authoring/rich-text-editor.md#main-pars-title-24)

   ![screen_shot_2018-03-22at120215](assets/screen_shot_2018-03-22at120215.png)

* Componente immagine

   ![screen_shot_2018-03-22at120252](assets/screen_shot_2018-03-22at120252.png)

   >[!NOTE]
   >
   >La modifica non funziona su un componente immagine vuoto.
   >
   >
   >È necessario [trascinare o caricare un’immagine (utilizzando Configura)](/help/sites-authoring/default-components-foundation.md#image) prima di poter iniziare a modificarla.

* Componente immagine (a schermo intero)

   [L’accesso alla modalità a tutto schermo](/help/sites-authoring/editing-content.md#edit-content-full-screen-mode) per il componente immagine consente di avere più spazio per modificare l’immagine oltre che per visualizzare opzioni di modifica aggiuntive, ad esempio **Launch Map (Avvia mappa)** e **Ripristina zoom**. Inoltre, lo schermo intero consente di selezionare i predefiniti di ritaglio.

   ![screen_shot_2018-03-22at120529](assets/screen_shot_2018-03-22at120529.png)

* I componenti formati da più di un componente di base, come il [Componente di base Testo e Immagine](/help/sites-authoring/default-components-foundation.md#text-image), richiedono prima di tutto di confermare quale insieme di opzioni di modifica desideri:

   ![chlimage_1-123](assets/chlimage_1-123.png)

### Trascinare risorse nel componente {#drag-and-drop-assets-into-component}

Per tipi di componenti specifici è possibile trascinare risorse dal browser risorse direttamente nel componente per aggiornare il contenuto:

| **Tipo risorsa** | **Tipo componente** |
|---|---|
| Immagine | Immagine |
| Documento | Scarica |
| Prodotto | Prodotto |
| Video | Flash |
| Frammenti di contenuto | Frammenti di contenuto |

## Modifica (contenuto) - Modalità a schermo intero {#edit-content-full-screen-mode}

Per tutti i componenti è possibile accedere alla (e uscire dalla) modalità a tutto tramite:

![](do-not-localize/chlimage_1-20.png)

Per esempio, il componente **Testo**:

![screen_shot_2018-03-22at121616](assets/screen_shot_2018-03-22at121616.png)

>[!NOTE]
>
>Per alcuni componenti, la modalità a schermo intero includerà più opzioni rispetto all’editor locale di base.

## Spostamento di un componente {#moving-a-component}

Per spostare un componente paragrafo:

1. Tocca o fai clic e tieni premuto per selezionare il paragrafo da spostare.
1. Trascina il paragrafo nella nuova posizione: in AEM verranno indicate le posizioni in cui è possibile spostare il paragrafo. Rilascia nella posizione desiderata.

   ![screen_shot_2018-03-22at121821](assets/screen_shot_2018-03-22at121821.png)

1. Il paragrafo è stato spostato.

>[!NOTE]
>
>Per spostare un componente puoi anche utilizzare [Taglia e Incolla](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste).

## Modificare il layout del componente {#edit-component-layout}

Invece di passare più volte dalla modalità di modifica alla [modalità di layout](/help/sites-authoring/responsive-layout.md) per regolare le impostazioni di un componente, è possibile selezionare l’azione **Layout**. Questo permette di modificare rapidamente il layout di quello specifico componente, senza uscire dalla modalità di modifica.

1. In modalità **Modifica** nella console Sites, quando si seleziona un componente viene visualizzata la sua barra degli strumenti.

   ![screen_shot_2018-03-22at133756](assets/screen_shot_2018-03-22at133756.png)

   Tocca o fai clic sull’azione **Layout** per modificare il layout del componente.

   ![](do-not-localize/chlimage_1-21.png)

1. Quando viene selezionata l’azione Layout:

   * Vengono visualizzate le maniglie di ridimensionamento del componente.
   * La barra degli strumenti dell’emulatore si trova nella parte superiore dello schermo.
   * Nella barra degli strumenti del componente vengono visualizzate le azioni di layout al posto delle azioni standard di modifica.

   ![screen_shot_2018-03-22at133843](assets/screen_shot_2018-03-22at133843.png)

   Ora puoi modificare il layout del componente, in modo analogo a come lo si modifica nella [modalità di layout](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode).

1. Dopo aver apportato le modifiche necessarie, fai clic sul pulsante **Chiudi** nel menu Azioni del componente per interrompere la modifica del layout del componente. La barra degli strumenti del componente torna al normale stato di modifica.

   ![](do-not-localize/screen_shot_2018-03-22at133920.png)

>[!NOTE]
>
>L’azione Layout è limitata al componente selezionato. Ad esempio, se stai modificando il layout di un componente e fai clic su un altro componente, per il componente appena selezionato viene visualizzata la barra degli strumenti di modifica standard (non quella di layout), mentre le maniglie di ridimensionamento e la barra degli strumenti dell’emulatore vengono nascosti.
>
>Se devi modificare il layout globale della pagina, interessando più componenti, passa alla [modalità di layout](/help/sites-authoring/responsive-layout.md).

## Componenti ereditati {#inherited-components}

I componenti ereditati possono essere il risultato di vari scenari, tra cui:

* [Gestione multisito](/help/sites-administering/msm.md)
* [Lanci](/help/sites-authoring/launches.md) (se basati su Live Copy).
* Componenti specifici, ad esempio il Sistema Paragrafo Ereditato all’interno di Geometrixx.

È possibile annullare (e quindi riattivare) l’ereditarietà. In base al componente, questo può essere disponibile da:

* **Live Copy**

   La barra degli strumenti del componente, se il componente si trova in una pagina che fa parte di una Live Copy o di un lancio (basato su una Live Copy). Per esempio:

   ![screen_shot_2018-03-22at134339](assets/screen_shot_2018-03-22at134339.png)

   L’opzione Annulla ereditarietà è disponibile:

   ![](do-not-localize/screen_shot_2018-03-22at134406.png)

   Se l’ereditarietà è già stata annullata, è invece disponibile l’opzione Riattiva ereditarietà:

   ![](do-not-localize/screen_shot_2018-03-22at134417.png)

   L’azione Rollout è disponibile anche nel blueprint o nella sorgente Live Copy: 

   ![](do-not-localize/screen_shot_2018-03-22at134516.png)

* **Un Sistema Paragrafo Ereditato**

   La finestra di dialogo di configurazione. Ad esempio, come con il Sistema Paragrafo Ereditato:

   ![chlimage_1-124](assets/chlimage_1-124.png)

## Modificare il modello di pagina {#editing-the-page-template}

Se la pagina è basata su un [modello modificabile](/help/sites-authoring/templates.md#editable-and-static-templates), puoi facilmente passare [all’editor modelli](/help/sites-authoring/templates.md#editing-templates-template-authors) selezionando **Modifica modello** nel menu [Informazioni pagina](/help/sites-authoring/author-environment-tools.md#page-information).

Se la pagina è basata su un [modello statico](/help/sites-authoring/templates.md#editable-and-static-templates), puoi passare a [Modalità Progettazione](/help/sites-authoring/default-components-designmode.md) utilizzando [selettore della modalità pagina](/help/sites-authoring/author-environment-tools.md#page-modes) sulla barra degli strumenti per abilitare/disabilitare i componenti da utilizzare nella pagina.

Puoi vedere facilmente su quale modello si basa la pagina quando la selezioni in [Vista a colonne](/help/sites-authoring/basic-handling.md#column-view) o [Vista a elenco](/help/sites-authoring/basic-handling.md#list-view).

## Stato della Live Copy   {#live-copy-status}

La [modalità di pagina Stato Live Copy](/help/sites-authoring/author-environment-tools.md#page-modes) consente di visualizzare una panoramica rapida dello stato della live copy e di quali componenti sono ereditati o no:

* Bordo verde: componente ereditato
* Bordo rosa: l’ereditarietà del componente è stata annullata

Esempio:

![screen_shot_2018-03-22at134820](assets/screen_shot_2018-03-22at134820.png)

## Aggiunta di annotazioni {#adding-annotations}

Le [Annotazioni](/help/sites-authoring/annotations.md) consentono a revisori e altri autori di fornire un riscontro sui contenuti. Spesso sono utilizzate a scopo di revisione e di convalida.

## Anteprima delle pagine   {#previewing-pages}

Esistono due opzioni per visualizzare in anteprima una pagina:

* [Modalità Anteprima](#preview-mode): un’anteprima rapida disponibile dalla stessa posizione

* [Visualizza come pubblicato](#view-as-published): un&#39;anteprima completa della pagina in una nuova scheda

>[!NOTE]
>
>* In modalità Modifica, i collegamenti nel contenuto sono visibili, ma non sono accessibili.
>* Per effettuare la navigazione tramite i collegamenti, utilizza una delle opzioni di anteprima.
>* Utilizza la [scelta rapida da tastiera](/help/sites-authoring/keyboard-shortcuts.md) `Ctrl-Shift-M` per passare dall’anteprima all’ultima modalità selezionata.
>


>[!NOTE]
>
>Il cookie della modalità WCM viene impostato per entrambe le opzioni.

### Modalità Anteprima {#preview-mode}

Quando si modifica il contenuto, è possibile visualizzare in anteprima la pagina mediante la [modalità di anteprima](/help/sites-authoring/author-environment-tools.md#page-modes). Questa modalità:

* Nasconde vari meccanismi di modifica per fornire un’indicazione rapida di come apparirà la pagina una volta pubblicata.
* Consente di utilizzare i collegamenti per la navigazione.
* **Non** aggiorna il contenuto della pagina.

Quando si creano contenuti, la modalità di anteprima è disponibile utilizzando l’icona in alto a destra dell’Editor pagina:

![chlimage_1-125](assets/chlimage_1-125.png)

### Visualizza come pubblicato {#view-as-published}

L’opzione **Visualizza come pubblicato**, è disponibile nel menu [Informazioni pagina](/help/sites-authoring/author-environment-tools.md#page-information). Permette di aprire la pagina in una nuova scheda, aggiornando il contenuto e visualizzando la pagina esattamente come apparirebbe nell’ambiente di pubblicazione.

## Blocco di una pagina   {#locking-a-page}

AEM consente di bloccare una pagina in modo da impedire che i contenuti possano essere modificati. Questa funzione è utile quando si devono apportare numerose modifiche a una pagina oppure se occorre bloccarla per un breve periodo di tempo.

Per bloccare una pagina è possibile utilizzare:

* La console **Sites**

   1. Seleziona la pagina con [modalità di selezione](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
   1. Seleziona l’icona Blocca.

   ![screen_shot_2018-03-22at134928](assets/screen_shot_2018-03-22at134928.png)

* **Editor pagina**

   1. Seleziona l’icona **Informazioni pagina** per aprire il menu.
   1. Seleziona l’opzione **Blocca pagina**.

Una volta eseguito il blocco le informazioni di visualizzazione della console vengono aggiornate e, durante la modifica, un simbolo a forma di lucchetto viene visualizzato nella barra degli strumenti.

![screen_shot_2018-03-22at135010](assets/screen_shot_2018-03-22at135010.png)

>[!CAUTION]
>
>Il blocco di pagina può essere eseguito quando si [impersona un utente](/help/sites-administering/security.md#impersonating-another-user). Tuttavia, una pagina bloccata in tale modalità può essere sbloccata solo dall’utente impersonato o da un utente amministratore.
>
>Non è consentito sbloccare le pagine bloccate impersonando l’utente che le ha boccate.

## Sblocco di una pagina {#unlocking-a-page}

La procedura di sblocco di una pagina è molto simile a quella di [blocco](#locking-a-page): una volta che la pagina è bloccata, le opzioni di blocco vengono sostituite da quelle di sblocco.

Nel menu Informazioni pagina è presente l’opzione **Sblocca** e l’icona Blocca nella console Sites viene sostituita dall’icona **Sblocca**.

![screen_shot_2018-03-22at134942](assets/screen_shot_2018-03-22at134942.png)

>[!CAUTION]
>
>Il blocco di pagina può essere eseguito quando si [impersona un utente](/help/sites-administering/security.md#impersonating-another-user). Tuttavia, una pagina bloccata in tale modalità può essere sbloccata solo dall’utente impersonato o da un utente amministratore.
>
>Non è consentito sbloccare le pagine bloccate impersonando l’utente che le ha boccate.

## Annullamento e ripristino di operazioni di modifica delle pagine {#undoing-and-redoing-page-edits}

Le icone seguenti consentono di annullare o ripristinare un’azione. Vengono visualizzate sulla barra degli strumenti quando necessario:

![](do-not-localize/screen_shot_2018-03-23at093614.png)

>[!NOTE]
>
>La [scelta rapida da tastiera](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) `Ctrl-Z` è inoltre disponibile per annullare le azioni di modifica della pagina.
>
>La scelta rapida da tastiera `Ctrl-Y` è disponibile anche per ripristinare le azioni di modifica della pagina.

>[!NOTE]
>
>Per informazioni sulle possibilità di annullare e ripristinare le modifiche apportate a una pagina, consulta [Annullamento e ripristino di operazioni di modifica delle pagine - La teoria](#undoing-and-redoing-page-edits-the-theory).

## Annullamento e ripristino di operazioni di modifica delle pagine - La teoria {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>L’amministratore di sistema può [configurare vari aspetti delle funzioni Annulla e Ripristina](/help/sites-administering/config-undo.md) in base ai requisiti particolari del caso in questione.

In AEM vengono memorizzate una cronologia delle azioni eseguite e la relativa sequenza, in modo che le varie azioni possano essere annullate nell’ordine di esecuzione; inoltre è possibile utilizzare l’opzione Ripristina per riapplicare una o più azioni annullate.

Se è selezionato un elemento nella pagina del contenuto (ad esempio un componente di testo) il comando Annulla o Ripristina si riferisce all’elemento selezionato.

Il comportamento dei comandi di annullamento e ripristino è simile a quello delle altre applicazioni software. Tali comandi consentono di ripristinare uno stato recente della pagina web in lavorazione. Se ad esempio si sposta un paragrafo di testo altrove nella pagina, è possibile ricorrere al comando Annulla per riportarlo nella posizione originale. Se successivamente constati che la posizione precedente era migliore, utilizza il comando Ripristina per “annullare l’annullamento”.

>[!NOTE]
>
>Operazioni disponibili:
>
>* Le azioni annullate possono essere ripristinate solo se dopo l’annullamento non sono state apportate altre modifiche alla pagina.
>* Per impostazione predefinita, è possibile annullare fino a 20 azioni di modifica.
>* Puoi eseguire le operazioni Annulla e Ripristina anche con le relative [scelte rapida da tastiera](/help/sites-authoring/page-authoring-keyboard-shortcuts.md).
>


I comandi Annulla e Ripristina possono essere utilizzati per i seguenti tipi di modifiche:

* Aggiunta, modifica, rimozione e spostamento di paragrafi
* Modifica locale del contenuto dei paragrafi
* Operazioni Copia, Taglia e Incolla per elementi all’interno di una pagina

Per i campi modulo generati dai componenti modulo non deve essere specificato alcun valore durante la creazione delle pagine. Pertanto i comandi Annulla/Ripristina non incidono sulle modifiche apportate ai valori di questo tipo di componenti. Ad esempio, non è possibile annullare la selezione di un valore in un elenco a discesa.

>[!NOTE]
>
>Per annullare e ripristinare le modifiche apportate a file e immagini sono necessarie autorizzazioni speciali.

>[!NOTE]
>
>La cronologia delle modifiche ai file e alle immagini viene conservata per almeno dieci ore. Oltre tale limite, la possibilità di annullare le modifiche non è garantita. L’amministratore può cambiare il tempo predefinito di dieci ore.
