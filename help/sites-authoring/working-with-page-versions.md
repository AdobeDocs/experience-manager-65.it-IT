---
title: Operazioni con le versioni delle pagine di contenuto
description: Creare, confrontare e ripristinare versioni di una pagina
uuid: 29e049f0-532c-4e3b-b64f-5be88ee6b08c
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1368347a-9b65-4cfc-87e1-62993dc627fd
docset: aem65
exl-id: cb7a9da2-7112-4ef0-b1cf-211a7df93625
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 66%

---

# Utilizzo delle versioni di una pagina  {#working-with-page-versions}

Il controllo delle versioni crea uno &quot;snapshot&quot; di una pagina in un momento specifico. Con il controllo delle versioni è possibile eseguire le seguenti operazioni:

* Crea una versione di una pagina.
* Ripristinare una versione precedente di una pagina per annullare, ad esempio, una modifica apportata a una pagina.
* Confronta la versione corrente di una pagina con una versione precedente con le differenze nel testo e nelle immagini evidenziate.

## Creazione di una nuova versione   {#creating-a-new-version}

Puoi creare una versione della risorsa da:

* la [Barra laterale Timeline](#creating-a-new-version-timeline)
* la [Crea](#creating-a-new-version-create-with-a-selected-resource) opzione (quando è selezionata una risorsa)

### Creazione di una nuova versione - Timeline {#creating-a-new-version-timeline}

1. Passa alla pagina per la quale desideri creare una versione.
1. Seleziona la pagina in [modalità di selezione](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. Apri **Timeline** colonna.
1. Tocca o fai clic sulla freccia accanto al campo del commento per visualizzare le opzioni:

   ![screen-shot_2019-03-05at112335](assets/screen-shot_2019-03-05at112335.png)

1. Seleziona **Salva come versione**.
1. Inserisci un **Etichetta** e **Commento** se necessario.

   ![chlimage_1-42](assets/chlimage_1-42.png)

1. Conferma la nuova versione selezionando **Crea**.

   Le informazioni nella timeline vengono aggiornate per indicare che si tratta di una nuova versione.

### Creazione di una nuova versione - Con una risorsa selezionata {#creating-a-new-version-create-with-a-selected-resource}

1. Passa alla pagina per la quale desideri creare una versione.
1. Seleziona la pagina in [modalità di selezione](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. Seleziona la **Crea** dalla barra degli strumenti.
1. Viene aperta una finestra di dialogo. Puoi immettere un’**etichetta** e un **commento**, se necessario:

   ![screen_shot_2012-02-15at105050am](assets/screen_shot_2012-02-15at105050am.png)

1. Conferma la nuova versione selezionando **Crea**.

   Viene aperta la timeline con le informazioni aggiornate per indicare che si tratta di una nuova versione.

## Ripristino delle versioni {#reinstating-versions}

Dopo aver creato una versione della pagina, esistono diversi metodi per ripristinare una versione precedente:

* L&#39;opzione **Ripristina questa versione** dalla barra [Timeline](/help/sites-authoring/basic-handling.md#timeline)

   Ripristinare una versione precedente di una pagina selezionata.

* L&#39;opzione **Ripristina** dalla [barra delle azioni](/help/sites-authoring/basic-handling.md#actions-toolbar) in alto

   * **Ripristina versione**

      Ripristina le versioni delle pagine specificate nella cartella attualmente selezionata; questo può anche includere il ripristino di pagine precedentemente eliminate.

   * **Ripristina albero**

      Ripristinare la versione dell&#39;intera struttura così come appariva a una data e un&#39;ora specificate può includere pagine precedentemente eliminate.

>[!NOTE]
>
>Durante il ripristino di una pagina, la versione creata sarà parte di un nuovo ramo.
>
>Per maggiore chiarezza:
>
>1. Crea versioni di qualsiasi pagina.
>1. Le etichette iniziali e i nomi dei nodi di versione saranno 1.0, 1.1, 1.2 e così via.
>1. Ripristina la prima versione, ovvero 1.0.
>1. Crea di nuovo nuove versioni.
>1. Le etichette generate e i nomi dei nodi saranno ora 1.0.0, 1.0.1, 1.0.2, ecc.


### Ripristina una versione {#revert-to-a-version}

Per **ripristinare** la pagina selezionata in una versione precedente:

1. Passa alla pagina da ripristinare a una versione precedente.
1. Seleziona la pagina in [modalità di selezione](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. Apri la colonna **Timeline** e seleziona **Mostra tutti** o **Versioni**. Vengono elencate le versioni disponibili per la pagina selezionata.
1. Seleziona la versione da ripristinare. Verranno visualizzate le opzioni possibili:

   ![Ripristina questa versione](assets/screen-shot_2019-03-05at112505.png)

1. Seleziona **Ripristina questa versione**. La versione selezionata viene ripristinata e le informazioni nella timeline vengono aggiornate.

### Ripristina versione {#restore-version}

Questo metodo può essere utilizzato per ripristinare versioni di pagine specifiche all&#39;interno della cartella corrente; questo può anche includere il ripristino di pagine eliminate precedentemente:

1. Vai alla cartella richiesta e [selezionala](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).

1. Seleziona **Ripristina**, quindi **Ripristina versione** dalla [barra delle azioni](/help/sites-authoring/basic-handling.md#actions-toolbar) in alto.

   >[!NOTE]
   >
   >Se:
   >
   >* hai selezionato una singola pagina che non ha mai avuto pagine figlie,
   >* o nessuna delle pagine della cartella dispone di versioni,

   >
   >Il display sarà quindi vuoto in quanto non sono disponibili versioni applicabili.

1. Vengono elencate le versioni disponibili:

   ![Ripristina versione - Elenco di tutte le pagine della cartella](/help/sites-authoring/assets/versions-restore-version-01.png)

1. Per una pagina specifica, utilizza il selettore a discesa in **RIPRISTINA VERSIONE** per selezionare la versione richiesta per la pagina.

   ![Ripristina versione - Seleziona versione](/help/sites-authoring/assets/versions-restore-version-02.png)

1. Nella visualizzazione principale, seleziona la pagina da ripristinare:

   ![Ripristina versione - Seleziona pagina](/help/sites-authoring/assets/versions-restore-version-03.png)

1. Seleziona **Ripristina** per la versione della pagina selezionata da ripristinare come versione corrente.

>[!NOTE]
>
>L’ordine in cui selezioni una pagina richiesta e la relativa versione è intercambiabile.

### Ripristina albero {#restore-tree}

Questo metodo può essere utilizzato per ripristinare una versione di una struttura in una data e in un&#39;ora specificate; possono essere incluse le pagine precedentemente eliminate:

1. Vai alla cartella richiesta e [selezionala](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).

1. Seleziona **Ripristina**, quindi **Ripristina struttura** dalla [barra delle azioni](/help/sites-authoring/basic-handling.md#actions-toolbar) in alto. Viene visualizzata la versione più recente della struttura:

   ![Ripristina albero](/help/sites-authoring/assets/versions-restore-tree-02.png)

1. Utilizza il selettore data e ora in **Versioni più recenti alla data** per selezionare un&#39;altra versione della struttura, quella da ripristinare.

1. Imposta il contrassegno **Pagine non versionate salvate** se necessario:

   * Se è attiva (selezionata), tutte le pagine senza versione verranno mantenute e non saranno interessate dal ripristino.

   * Se non è attiva (deselezionata), tutte le pagine non versionate verranno rimosse in quanto non esistevano nella struttura versionata.

1. Seleziona **Ripristina** per la versione selezionata della struttura da ripristinare come versione *attuale*.

## Anteprima di una versione   {#previewing-a-version}

Puoi visualizzare in anteprima una versione specifica:

1. Passa alla pagina da confrontare.
1. Seleziona la pagina in [modalità di selezione](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. Apri la colonna **Timeline** e seleziona **Mostra tutti** o **Versioni**.
1. Vengono elencate le versioni disponibili. Seleziona la versione da visualizzare in anteprima:

   ![screen-shot_2019-03-05at112505-1](assets/screen-shot_2019-03-05at112505-1.png)

1. Seleziona **Anteprima**. La pagina verrà visualizzata in una nuova scheda.

   >[!CAUTION]
   >
   >Se una pagina è stata spostata, non è più possibile eseguire un’anteprima sulle versioni eseguite prima dello spostamento.
   >
   >* Se riscontri dei problemi con un&#39;anteprima, controlla il [Timeline](/help/sites-authoring/basic-handling.md#timeline) per verificare se la pagina è stata spostata.


## Confronto di una versione con la pagina corrente {#comparing-a-version-with-current-page}

Per confrontare una versione precedente con la pagina corrente:

1. Passa alla pagina da confrontare.
1. Seleziona la pagina in [modalità di selezione](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. Apri la colonna **Timeline** e seleziona **Mostra tutti** o **Versioni**.
1. Vengono elencate le versioni disponibili. Seleziona la versione da confrontare:

   ![screen-shot_2019-03-05at112505-2](assets/screen-shot_2019-03-05at112505-2.png)

1. Seleziona **Confronta con corrente**. La [differenze tra pagine](/help/sites-authoring/page-diff.md) apre e visualizza le differenze.

## Timewarp   {#timewarp}

Timewarp è una funzione progettata per simulare lo stato *di pubblicazione* di una pagina in specifici momenti nel passato.

>[!TIP]
>
>[Timewarp può essere utilizzato anche con Lanci per visualizzare in anteprima il futuro](/help/sites-authoring/launches.md) quando si esegue AEM 6.5.10.0 o versione successiva.

Poiché la creazione di contenuti è un processo continuo e collaborativo, lo scopo di Timewarp è di consentire agli autori di tenere traccia del sito web pubblicato nel tempo, in modo da comprendere in che modo è cambiato il contenuto. Questa funzione utilizza le versioni delle pagine per determinare lo stato dell’ambiente di pubblicazione.

Per effettuare questo collegamento:

* Il sistema cerca la versione della pagina che era attiva al momento selezionato.
* In altre parole, la versione mostrata era stata creata/attivata *prima* del momento temporale selezionato in Timewarp.
* Quando si passa a una pagina che è stata successivamente eliminata, questa viene riprodotta purché nell’archivio siano ancora disponibili le precedenti versioni di tale pagina.
* Se non viene individuata alcuna versione pubblicata, Timewarp ripristina lo stato corrente della pagina nell’ambiente di authoring, in modo da evitare un errore 404 di pagina non trovata, che impedirebbe la navigazione.

### Utilizzo di Timewarp {#using-timewarp}

Timewarp è un [modalità](/help/sites-authoring/author-environment-tools.md#page-modes) dell’editor di pagine. Per avviarlo, è sufficiente attivarlo come per qualsiasi altra modalità.

1. Avvia l’editor per la pagina in cui desideri avviare Timewarp, quindi seleziona **Timewarp** nella selezione della modalità.

   ![wpv-01](assets/wwpv-01.png)

1. Nella finestra di dialogo, imposta una data e un’ora di destinazione e tocca o fai clic su **Imposta data**. Se non si seleziona un’ora, per impostazione predefinita verrà utilizzata l’ora corrente.

   ![wpv-02](assets/wwpv-02.png)

1. La pagina viene visualizzata in base alla data impostata. La modalità Timewarp è indicata dalla barra di stato blu nella parte superiore della finestra. Utilizza i collegamenti nella barra di stato per selezionare una nuova data di destinazione o uscire dalla modalità Timewarp.

   ![wpv-03](assets/wwpv-03.png)

### Limitazioni di Timewarp {#timewarp-limitations}

Timewarp semplifica al massimo la riproduzione di una pagina in un determinato momento. Tuttavia, a causa delle complessità dell’authoring continuo di contenuti in AEM, questo non è sempre possibile. Tieni presenti queste limitazioni quando utilizzi Timewarp.

* **Timewarp funziona in base alle pagine pubblicate**: Timewarp funziona correttamente solo se la pagina è stata già pubblicata. In caso contrario viene mostrata la pagina corrente nell’ambiente di authoring.
* **Timewarp utilizza le versioni di pagina**: se passi a una pagina che è stata rimossa o eliminata dall’archivio, questa verrà riprodotta correttamente se nell’archivio sono ancora disponibili versioni precedenti della pagina.
* **Le versioni rimosse influiscono su Timewarp**: se dalla directory archivio sono state rimosse delle versioni, Timewarp non può mostrare la visualizzazione corretta.

* **Timewarp è di sola lettura**: non è possibile modificare la versione precedente della pagina, ma solo visualizzarla. Se desideri ripristinare la versione precedente, devi farlo manualmente utilizzando la funzione di [ripristino](#reverting-to-a-page-version).

* **Timewarp si basa solo sul contenuto della pagina**: se sono stati modificati alcuni elementi (come codice, css, risorse/immagini ecc.) per il rendering del sito web, la visualizzazione sarà diversa da come era all’origine, poiché per tali elementi non vengono conservate precedenti versioni nell’archivio.

>[!CAUTION]
>
>Timewarp è uno strumento utile per aiutare gli autori a comprendere e creare i propri contenuti. Non deve essere utilizzato come registro di controllo o per fini legali.
