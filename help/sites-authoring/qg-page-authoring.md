---
title: Guida rapida all’authoring delle pagine
seo-title: Quick Guide to Authoring Pages
description: Guida rapida di alto livello alle azioni chiave per l’authoring dei contenuti di una pagina
seo-description: A quick, high-level guide to the key actions of authoring page content
uuid: ef7ab691-f80d-4eeb-9f4a-afbf1bc83669
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 2d35a2a4-0c8c-4b16-99a6-c6e6d66446dc
docset: aem65
exl-id: a7e16555-9bbe-4da2-817c-4495a0193f3f
source-git-commit: d045fc1ac408f992d594a4cb68d1c4eeae2b0de1
workflow-type: tm+mt
source-wordcount: '1558'
ht-degree: 45%

---

# Guida rapida all’authoring delle pagine{#quick-guide-to-authoring-pages}

Queste procedure sono intese come guida rapida (di alto livello) alle azioni chiave per la creazione di contenuti di pagina nell’AEM.

Si occupano di:

* Non sono intese come copertura completa.
* Fornisci collegamenti alla documentazione dettagliata.

Per maggiori dettagli sull’authoring con AEM consulta:

* [Primi passaggi per gli autori](/help/sites-authoring/first-steps.md)
* [Authoring delle pagine](/help/sites-authoring/page-authoring.md)

## Alcuni suggerimenti rapidi {#a-few-quick-hints}

Prima di fornire una panoramica delle specifiche, ecco una piccola raccolta di suggerimenti generali che vale la pena tenere a mente.

### Console Sites {#sites-console}

* **Crea**

   * Questo pulsante è disponibile in molte console; le opzioni visualizzate sono contestuali e quindi possono variare a seconda dello scenario.

* Riordinamento delle pagine in una cartella

   * Questa operazione può essere eseguita in [Vista a elenco](/help/sites-authoring/basic-handling.md#list-view). Le modifiche vengono applicate e visualizzate in altre viste.

#### Authoring delle pagine {#page-authoring}

* Collegamenti di navigazione

   * ***I collegamenti non sono disponibili per la navigazione*** quando sei in **Modifica** modalità. Per navigare con i collegamenti, è necessario [anteprima della pagina](/help/sites-authoring/editing-content.md#previewing-pages) utilizzando:

      * [Modalità Anteprima](/help/sites-authoring/editing-content.md#preview-mode)
      * [Visualizza come pubblicato](/help/sites-authoring/editing-content.md#view-as-published)

* Le versioni non vengono avviate/create dall’editor di pagine, questa operazione è ora eseguita dalla console Sites (tramite **Crea** o [Timeline](/help/sites-authoring/basic-handling.md#timeline) per una risorsa selezionata).

>[!NOTE]
>
>Esistono diverse scelte rapide da tastiera che possono semplificare l’esperienza di authoring.
>
>* [Scelte rapide da tastiera durante la modifica delle pagine](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
>* [Scelte rapide da tastiera per le console](/help/sites-authoring/keyboard-shortcuts.md)
>

### Ricerca di una pagina {#finding-your-page}

Sono disponibili vari aspetti per individuare una pagina. Puoi navigare e/o eseguire ricerche:

1. Apri **Sites** console (utilizzando il **Sites** opzione in [Navigazione globale](/help/sites-authoring/basic-handling.md#global-navigation)) - viene attivato (a discesa) quando selezioni il collegamento Adobe Experience Manager (in alto a sinistra).

1. Spostati verso il basso all’interno della struttura toccando/facendo clic sulla pagina appropriata. La modalità di rappresentazione delle risorse di pagina dipende dalla vista che stai utilizzando, [A schede, Elenco o Colonna](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources):

   ![screen_shot_2018-03-21at160214](assets/screen_shot_2018-03-21at160214.png)

1. Per spostarti in alto nella struttura, usa le [breadcrumb nell’intestazione](/help/sites-authoring/basic-handling.md#theheaderwithbreadcrumbs), che permettono di tornare alla posizione selezionata:

   ![qgtap-01](assets/qgtap-01.png)

1. È inoltre possibile [Ricerca](/help/sites-authoring/search.md) per una pagina. Puoi selezionare la pagina dai risultati mostrati.

   ![qgtap-03](assets/qgtap-03.png)

### Creazione di una nuova pagina {#creating-a-new-page}

A [creare una pagina](/help/sites-authoring/managing-pages.md#creating-a-new-page):

1. [Passa alla posizione](#finding-your-page) dove desideri creare la pagina.
1. Utilizza il **Crea** e quindi seleziona **Pagina** dall’elenco:

   ![qgtap-02](assets/qgtap-02.png)

1. Verrà aperta la procedura guidata che ti guiderà attraverso la raccolta delle informazioni necessarie quando [creazione di una nuova pagina](/help/sites-authoring/managing-pages.md#creating-a-new-page). Seguire le istruzioni visualizzate.

### Selezione della pagina per ulteriori azioni   {#selecting-your-page-for-further-action}

Puoi selezionare una pagina in modo da poter intervenire su di essa. Quando si seleziona una pagina, la barra degli strumenti viene aggiornata automaticamente in modo da visualizzare le azioni relative a tale risorsa.

La modalità di selezione di una pagina dipende dalla visualizzazione utilizzata nella console:

1. Vista a colonne:

   * Tocca/fai clic sulla miniatura della risorsa richiesta; sulla miniatura compare un segno di spunta per indicare che è stata selezionata.

1. Vista a elenco:

   * Tocca/fai clic sulla miniatura della risorsa richiesta; sulla miniatura compare un segno di spunta per indicare che è stata selezionata.

1. Vista a schede:

   * Entra nella modalità di selezione per [selezione della risorsa richiesta](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources) con:

      * Dispositivo mobile: toccare e tenere premuto
      * Desktop: il [azione rapida](/help/sites-authoring/basic-handling.md#quick-actions) - icona di spunta:

   ![screen_shot_2018-03-21at160503](assets/screen_shot_2018-03-21at160503.png)

   * Sulla scheda compare un segno di spunta per indicare che è stata selezionata la pagina.

   >[!NOTE]
   >
   >Una volta nella modalità di selezione, **Seleziona** (un segno di spunta) verrà modificata in **Deseleziona** (croce).

### Azioni rapide (solo vista a schede/desktop) {#quick-actions-card-view-desktop-only}

Sono disponibili delle [Azioni rapide](/help/sites-authoring/basic-handling.md#quick-actions):

1. [Passa alla pagina](#finding-your-page) sulla quale desideri intervenire.
1. Passa il puntatore del mouse sulla scheda che rappresenta la risorsa desiderata; verranno visualizzate le azioni rapide:

   ![screen_shot_2018-03-21at160503-1](assets/screen_shot_2018-03-21at160503-1.png)

### Modifica del contenuto delle pagine {#editing-your-page-content}

1. [Passa alla pagina](#finding-your-page) da modificare.
1. [Apri la pagina per la modifica](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing) tramite l’icona Modifica (matita):

   ![screen_shot_2018-03-21at160607](assets/screen_shot_2018-03-21at160607.png)

   È accessibile da:

   * [Azioni rapide (solo vista a schede/desktop)](#quick-actions-card-view-desktop-only) per la risorsa appropriata.
   * La barra degli strumenti, se la [pagina è stata selezionata](#selectiingyourpageforfurtheraction).

1. All’apertura dell’editor, puoi:

   * [Aggiungere un nuovo componente alla pagina](/help/sites-authoring/editing-content.md#inserting-a-component):

      * apertura del pannello laterale
      * selezionando la scheda componenti (la [browser componenti](/help/sites-authoring/author-environment-tools.md#components-browser))
      * trascinamento del componente richiesto sulla pagina.

     Il pannello laterale può essere aperto (e chiuso) con:

     ![Apri pannello laterale](do-not-localize/screen_shot_2018-03-21at160738.png)

   * [Modificare il contenuto di un componente esistente](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) sulla pagina:

      * Apri la barra degli strumenti del componente toccando o facendo clic. Utilizza il **Modifica** (matita) per aprire la finestra di dialogo
      * Apri l’editor locale per il componente toccando e tenendo premuto o facendo doppio clic con il tasto Slow. Vengono visualizzate le azioni disponibili (per alcuni componenti è una selezione limitata).
      * Per visualizzare tutte le azioni disponibili, entra in modalità a schermo intero utilizzando:

     ![Modalità a tutto schermo](do-not-localize/screen_shot_2018-03-21at160706.png)

   * [Configurare le proprietà di un componente esistente](/help/sites-authoring/editing-content.md#component-edit-dialog)

      * Apri la barra degli strumenti del componente toccando o facendo clic. Utilizza il **Configura** (chiave inglese) per aprire la finestra di dialogo.

   * [Spostare un componente](/help/sites-authoring/editing-content.md#moving-a-component) oppure:

      * Trascina il componente richiesto nella nuova posizione.
      * Apri la barra degli strumenti del componente toccando o facendo clic. Utilizza le icone **Taglia** e quindi **Incolla** dove richiesto.

   * [Copiare (e incollare)](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) un componente:

      * Apri la barra degli strumenti del componente toccando o facendo clic. Utilizza le icone **Taglia** e quindi **Incolla** come richiesto.

   >[!NOTE]
   >
   >È possibile utilizzare **Incolla** per collocare i componenti sulla stessa pagina o su una pagina differente. Se si incolla un componente in una pagina che era già aperta prima dell’operazione Taglia o Copia, sarà necessario aggiornare la pagina.

   * [Eliminare](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) un componente:

      * Apri la barra degli strumenti del componente toccando o facendo clic, quindi utilizza l’icona **Elimina**.

   * [Aggiungere annotazioni](/help/sites-authoring/annotations.md#annotations) alla pagina:

      * Seleziona la modalità **Annota** (icona a forma di fumetto). Aggiungi le annotazioni utilizzando l’icona **Aggiungi annotazione** (segno più). Esci dalla modalità di annotazione utilizzando la X in alto a destra.

     ![Annotazioni](do-not-localize/screen_shot_2018-03-21at160813.png)

   * [Visualizzare l’anteprima di una pagina](/help/sites-authoring/editing-content.md#preview-mode) (per vedere come apparirà nell’ambiente di pubblicazione)

      * Seleziona **Anteprima** dalla barra degli strumenti.

   * Torna alla modalità di modifica (o seleziona un’altra modalità) utilizzando **Modifica** selettore a discesa.

   >[!NOTE]
   >
   >Per navigare utilizzando i collegamenti presenti nel contenuto, è necessario utilizzare [Modalità Anteprima](/help/sites-authoring/editing-content.md#preview-mode).

### Modifica delle proprietà pagina   {#editing-the-page-properties}

Esistono due metodi (principali) di [modifica delle proprietà di pagina](/help/sites-authoring/editing-page-properties.md):

* Dalla console **Sites**:

   1. [Passa alla pagina](#finding-your-page) desideri pubblicare.
   1. Seleziona la **Proprietà** da:

      * [Azioni rapide (solo vista a schede/desktop)](#quick-actions-card-view-desktop-only) per la risorsa appropriata.
      * La barra degli strumenti, se la [pagina è stata selezionata](#selectiingyourpageforfurtheraction).

  ![screen_shot_2018-03-21at160850](assets/screen_shot_2018-03-21at160850.png)

   1. Verranno visualizzate le proprietà di pagina. È possibile apportare le modifiche desiderate e poi selezionare Salva per applicarle

* Quando [modifica della pagina](#editing-your-page-content):

   1. Apri **Informazioni pagina** menu.
   1. Seleziona **Apri proprietà** per aprire la finestra di dialogo per la modifica delle proprietà.

  ![screen_shot_2018-03-21at160920](assets/screen_shot_2018-03-21at160920.png)

### Pubblicazione della pagina (o annullamento della pubblicazione) {#publishing-your-page-or-unpublishing}

Esistono due metodi principali per [pubblicazione della pagina](/help/sites-authoring/publishing-pages.md) (e anche di annullamento della pubblicazione):

* Dalla console **Sites**:

   1. [Passa alla pagina](#finding-your-page) desideri pubblicare.
   1. Seleziona l’icona **Pubblicazione rapida** da:

      * [Azioni rapide (solo vista a schede/desktop)](#quick-actions-card-view-desktop-only) per la risorsa appropriata.
      * La barra degli strumenti, se la [pagina è stata selezionata](#selectiingyourpageforfurtheraction) (consente anche di accedere a [Pubblica più tardi](/help/sites-authoring/publishing-pages.md#main-pars-title-12)).

  ![screen_shot_2018-03-21at160957](assets/screen_shot_2018-03-21at160957.png)

* Quando [modifica della pagina](#editing-your-page-content):

   1. Apri **Informazioni pagina** menu.
   1. Seleziona **Pubblica pagina**.

  ![screen_shot_2018-03-21at161026](assets/screen_shot_2018-03-21at161026.png)

* L’annullamento della pubblicazione di una pagina dalla console può essere eseguito solo tramite l’opzione **Gestisci pubblicazione**, disponibile solamente nella barra degli strumenti (non tramite le azioni rapide).

  Il **Annulla pubblicazione pagina** è ancora disponibile tramite il **Informazioni pagina** nell’editor.

  ![screen_shot_2018-03-21at161059](assets/screen_shot_2018-03-21at161059.png)

  Consulta [Pubblicazione delle pagine](/help/sites-authoring/publishing-pages.md#unpublishing-pages) per ulteriori informazioni.

### Spostamento, utilizzo di Copia e Incolla o eliminazione della pagina   {#move-copy-and-paste-or-delete-your-page}

Queste azioni possono essere tutte attivate da:

1. [Passa alla pagina](#finding-your-page) si desidera spostare, copiare, incollare o eliminare.
1. Seleziona l’icona Copia (e quindi Incolla), Sposta o Elimina, a seconda delle necessità, utilizzando:

   * [Azioni rapide (solo vista a schede/desktop)](#quick-actions-card-view-desktop-only) per la risorsa richiesta.
   * La barra degli strumenti, se la [pagina è stata selezionata](#selecting-your-page-for-further-action).

   Quindi, a seconda dell’azione:

   * Copia:

      * Passa alla nuova posizione e incolla.

   * Sposta:

      * Viene visualizzata la procedura guidata per raccogliere le informazioni necessarie per spostare la pagina. Seguire le istruzioni visualizzate.

   * Elimina:

      * Ti viene chiesto di confermare l’azione.

   >[!NOTE]
   >
   >Elimina non è disponibile come azione rapida.

### Blocco della pagina (e successivo sblocco) {#locking-your-page-then-unlocking}

[Il blocco di una pagina](/help/sites-authoring/editing-content.md#locking-a-page) non consente ad altri autori di utilizzarla mentre vi lavori. L’icona o il pulsante Blocca (e Sblocca) è disponibile:

* La barra degli strumenti, se la [pagina è stata selezionata](#selecting-your-page-for-further-action).
* Il [Menu a discesa Informazioni pagina](#editing-the-page-properties) durante la modifica di una pagina.
* La barra degli strumenti della pagina durante la modifica di una pagina (quando la pagina è bloccata)

Ad esempio, l’icona Blocca ha l’aspetto di un lucchetto chiuso:

![screen_shot_2018-03-21at161124](assets/screen_shot_2018-03-21at161124.png)

### Accesso ai riferimenti di pagina {#accessing-page-references}

[Accesso rapido ai riferimenti](/help/sites-authoring/author-environment-tools.md#references) in una pagina o da una pagina sono disponibili nella barra laterale Riferimenti.

1. Seleziona l’icona **Riferimenti** dalla barra degli strumenti (prima o dopo aver [selezionato la pagina](#selecting-your-page-for-further-action)):

   ![screen_shot_2018-03-21at161210](assets/screen_shot_2018-03-21at161210.png)

   Verrà visualizzato un elenco di tipi di riferimenti:

   ![schermata_2019-03-05at114412](assets/screen-shot_2019-03-05at114412.png)

1. Tocca o fai clic sul tipo di riferimento richiesto per visualizzare ulteriori dettagli e, se necessario, per intraprendere ulteriori azioni.

### Creazione di una versione della pagina   {#creating-a-version-of-your-page}

Per creare una [versione](/help/sites-authoring/working-with-page-versions.md) di una pagina:

1. Per aprire la barra laterale Timeline, seleziona l’icona **[Timeline](/help/sites-authoring/basic-handling.md#timeline)** dalla barra degli strumenti (prima o dopo aver [selezionato la pagina](#selecting-your-page-for-further-action)):

   ![screen_shot_2018-03-21at161355](assets/screen_shot_2018-03-21at161355.png)

1. Tocca o fai clic sulla freccia su in basso a destra della colonna Timeline per visualizzare pulsanti aggiuntivi, tra cui **Salva come versione**.

   ![schermata_2019-03-05at114600](assets/screen-shot_2019-03-05at114600.png)

1. Seleziona **Salva come versione** quindi **Crea**.

### Ripristino/confronto di una versione della pagina {#restoring-comparing-a-version-of-your-page}

Lo stesso meccanismo di base viene utilizzato per il ripristino e/o il confronto tra diverse versioni di una pagina:

1. Seleziona l’icona **[Timeline](/help/sites-authoring/basic-handling.md#timeline)** dalla barra degli strumenti (prima o dopo aver [selezionato la pagina](#selecting-your-page-for-further-action)):

   ![screen_shot_2018-03-21at161355-1](assets/screen_shot_2018-03-21at161355-1.png)

   Se una versione della pagina è già stata salvata, viene elencata nella Timeline.

1. Tocca o fai clic sulla versione da ripristinare. Verranno visualizzati pulsanti di azione aggiuntivi:

   * **Ripristina questa versione**

      * La versione viene ripristinata.

   * **Mostra differenze**

      * La pagina viene aperta evidenziando le differenze (tra le due versioni).
