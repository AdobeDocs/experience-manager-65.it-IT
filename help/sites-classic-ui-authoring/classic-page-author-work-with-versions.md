---
title: Utilizzo delle versioni di una pagina
seo-title: Working with Page Versions
description: Quando si crea una versione, viene creata un’istantanea di una pagina in un particolare momento.
seo-description: Versioning creates a "snapshot" of a page at a specific point in time.
uuid: 06e112cd-e4ae-4ee0-882d-7009f53ac85b
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 48936115-4be2-4b0c-81ce-d61e43e4535d
docset: aem65
exl-id: 4eb0de5e-0306-4166-9cee-1297a5cd14ce
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 91%

---

# Utilizzo delle versioni di una pagina  {#working-with-page-versions}

Quando si crea una versione, viene creata un’istantanea di una pagina in un particolare momento. La funzione di gestione delle versioni consente di effettuare le seguenti operazioni:

* Creare una versione di una pagina.
* Ripristinare una versione precedente di una pagina, ad esempio per annullare una modifica apportata alla pagina.
* Confrontare la versione corrente di una pagina con una versione precedente, evidenziando le differenze nel testo e nelle immagini.

## Creazione di una nuova versione   {#creating-a-new-version}

Per creare una nuova versione di una pagina:

1. Nel browser, apri la pagina per la quale desideri creare una nuova versione.
1. Nella barra laterale, seleziona la scheda **Gestione versioni**, quindi la sottoscheda **Crea versione**.

   ![screen_shot_2012-02-14at40259pm](assets/screen_shot_2012-02-14at40259pm.png)

1. Inserisci un **Commento** (facoltativo).
1. Per impostare un’etichetta per la versione (facoltativa), fai clic sul pulsante **Altro >>** e impostare **Etichetta** per assegnare un nome alla versione. Se l’etichetta non è impostata, la versione è un numero incrementato automaticamente.
1. Fai clic su **Crea versione**. Sulla pagina viene visualizzato un messaggio in grigio; ad esempio: La versione 1.2 creata per: Camicie.

>[!NOTE]
>
>Quando la pagina viene attivata, viene automaticamente creata una versione.

## Ripristino di una versione di una pagina dalla barra laterale {#restoring-a-page-version-from-sidekick}

Per ripristinare una versione precedente della pagina:

1. Apri la pagina di cui desideri ripristinare una versione precedente.
1. Nella barra laterale seleziona la scheda **Gestione versioni**, quindi la sottoscheda **Ripristina versione**.

   ![screen_shot_2012-02-14at42949pm](assets/screen_shot_2012-02-14at42949pm.png)

1. Selezionate la versione da ripristinare e selezionate **Ripristina**.

## Ripristino di una versione di una pagina dalla console {#restoring-a-page-version-from-the-console}

Questo metodo può essere utilizzato per ripristinare una versione di una pagina o pagine precedentemente eliminate:

1. Nella console **Siti Web** individua e seleziona la pagina da ripristinare.
1. Nel menu principale seleziona **Strumenti**, quindi **Ripristina**:

   ![screen_shot_2012-02-08at41326pm](assets/screen_shot_2012-02-08at41326pm.png)

1. Se selezioni **Ripristina versione**, vengono elencate le versioni precedenti dei documenti presenti nella cartella corrente. Anche se una pagina è stata eliminata, ne viene elencata l’ultima versione:

   ![screen_shot_2012-02-08at45743pm](assets/screen_shot_2012-02-08at45743pm.png)

1. Seleziona la versione da ripristinare e fai clic su **Ripristina**. AEM ripristina le versioni o gli alberi selezionati.

### Ripristino di una struttura ad albero dalla console {#restoring-a-tree-from-the-console}

Questo metodo può essere utilizzato per ripristinare una versione di una pagina o pagine precedentemente eliminate:

1. Nella console **Siti Web** individua e seleziona la cartella da ripristinare.
1. Nel menu principale seleziona **Strumenti**, quindi **Ripristina**.
1. Seleziona **Ripristina albero** per aprire la finestra di dialogo in cui selezionare la struttura ad albero da ripristinare:

   ![screen_shot_2012-02-08at45743pm-1](assets/screen_shot_2012-02-08at45743pm-1.png)

1. Fai clic su **Ripristina**. AEM ripristina la struttura ad albero selezionata.

## Confronto con una versione precedente {#comparing-with-a-previous-version}

Per confrontare la versione corrente della pagina con una versione precedente:

1. Nel browser, apri la pagina da confrontare con una versione precedente.
1. Nella barra laterale, seleziona la **Controllo delle versioni** , quindi la **Ripristina versione** n sottoscheda.

   ![screen_shot_2012-02-14at42949pm-1](assets/screen_shot_2012-02-14at42949pm-1.png)

1. Seleziona la versione da utilizzare per il confronto e fai clic sul pulsante **Diff**.
1. Le differenze tra la versione corrente e quella selezionata vengono visualizzate come segue:

   * Il testo eliminato è barrato in rosso.
   * Il testo aggiunto è evidenziato in verde.
   * Le immagini aggiunte o eliminate sono circondate da una cornice verde.

   ![chlimage_1-75](assets/chlimage_1-75.png)

1. Nella barra laterale seleziona la sottoscheda **Ripristina versione** e fai clic sul pulsante **&lt;&lt;Indietro** per visualizzare la versione corrente.

## Timewarp   {#timewarp}

Timewarp è una funzione progettata per simulare lo stato ***di pubblicazione*** di una pagina in specifici momenti nel passato.

Questo consente di tenere tracciare del sito pubblicato in un particolare momento. Le attivazioni pagina vengono usate per determinare lo stato dell’ambiente di pubblicazione.

Per effettuare questo collegamento:

* Il sistema cerca la versione della pagina che era attiva nel momento temporale selezionato.
* In altre parole, la versione mostrata era stata creata/attivata *prima* del momento temporale selezionato in Timewarp.
* Quando si passa a una pagina che è stata successivamente eliminata, questa viene riprodotta purché nella directory archivio siano ancora disponibili le precedenti versioni di tale pagina.
* Se non viene trovata alcuna versione pubblicata, Timewarp ripristina lo stato corrente della pagina nell’ambiente di creazione (in modo da evitare un errore 404 di pagina non trovata, che impedirebbe di continuare la navigazione).

>[!NOTE]
>
>Se dalla directory archivio sono state rimosse delle versioni, Timewarp non può mostrare la visualizzazione corretta. Inoltre, se sono stati modificati alcuni elementi (come codice, css, immagini ecc.) per la riproduzione del sito Web, la visualizzazione sarà diversa da come era all’origine, poiché per tali elementi non vengono conservate precedenti versioni nella directory archivio.

### Utilizzo del calendario Timewarp {#using-the-timewarp-calendar}

Timewarp è disponibile dalla barra laterale.

La versione Calendario viene usata per visualizzare uno specifico giorno:

1. Aprite la scheda **Gestione versioni** e fate clic su **Timewarp** (verso il fondo della barra laterale). Viene visualizzata la seguente finestra di dialogo:

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. Specificate la data e ora desiderata con gli appositi selettori e fate clic su **Vai**.

   Timewarp presenta la pagina così come era nel suo stato pubblicato prima o alla data specificata.

   >[!NOTE]
   >
   >Timewarp funziona correttamente solo se la pagina era effettivamente stata precedentemente pubblicata. In caso contrario viene mostrata la pagina corrente nell’ambiente di authoring.

   >[!NOTE]
   >
   >Se passi a una pagina che è stata rimossa o eliminata dall’archivio, questa verrà riprodotta correttamente se nell’archivio sono ancora disponibili versioni precedenti della pagina.

   >[!NOTE]
   >
   >Non è possibile modificare la versione precedente della pagina, ma solo visualizzarla. Se desideri ripristinare la versione precedente, devi farlo manualmente utilizzando la funzione di [ripristino](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoring-a-page-version-from-sidekick).

1. Dopo aver visualizzato la pagina, fai clic su:

   * **Esci dal Timewarp** per uscire e tornare alla pagina corrente in modalità di creazione.
   * [Mostra timeline](#using-the-timewarp-timeline) consente di visualizzare la timeline.

   ![chlimage_1-77](assets/chlimage_1-77.png)

### Utilizzo della timeline Timewarp {#using-the-timewarp-timeline}

La versione timeline permette di vedere una panoramica delle attività di pubblicazione effettuate sulla pagina.

Per visualizzare la timeline di un documento:

1. Per mostrare la timeline potete effettuare una delle seguenti operazioni:

   1. Apri la scheda **Gestione versioni** e fai clic su **Timewarp** (verso il fondo della barra laterale).

   1. Utilizza la finestra di dialogo della barra laterale visualizzata dopo [l’utilizzo del calendario Timewarp](#using-the-timewarp-calendar).

1. Fate clic su **Mostra timeline**. Viene visualizzata la timeline del documento, ad esempio:

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. Selezionate e spostate (trascinate) la timeline per spostare la timeline del documento.

   * Le linee indicano le versioni pubblicate.
Quando una pagina viene attivata, inizia una nuova inea. Ogni volta che il documento viene modificato, compare un nuovo colore.
Nell’esempio di seguito, la linea rossa indica che la pagina è stata modificata nel periodo di tempo della versione iniziale verde e la linea gialla indica che la pagina è stata modificata nel corso della versione rossa, e così via.

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. Clic:

   1. **Vai** per mostrare il contenuto della pagina pubblicata al momento selezionato.
   1. Quando tale contenuto è visualizzato, **Esci dal Timewarp** consente di uscire e tornare alla pagina corrente in modalità di authoring.

### Limitazioni di Timewarp {#timewarp-limitations}

Timewarp semplifica al massimo la riproduzione di una pagina in un determinato momento. Tuttavia, a causa delle complessità dell’authoring continuo di contenuti in AEM, questo non è sempre possibile. Tieni presenti queste limitazioni quando utilizzi Timewarp.

* **Timewarp funziona in base alle pagine pubblicate**: Timewarp funziona correttamente solo se la pagina è stata già pubblicata. In caso contrario viene mostrata la pagina corrente nell’ambiente di authoring.
* **Timewarp utilizza le versioni di pagina**: se passi a una pagina che è stata rimossa o eliminata dall’archivio, questa verrà riprodotta correttamente se nell’archivio sono ancora disponibili versioni precedenti della pagina.
* **Le versioni rimosse influiscono su Timewarp**: se dalla directory archivio sono state rimosse delle versioni, Timewarp non può mostrare la visualizzazione corretta.

* **Timewarp è di sola lettura**: non è possibile modificare la versione precedente della pagina, ma solo visualizzarla. Se desideri ripristinare la versione precedente, devi farlo manualmente utilizzando la funzione di [ripristino](#main-pars-title-1).

* **Timewarp si basa solo sul contenuto della pagina**: se sono stati modificati alcuni elementi (come codice, css, risorse/immagini ecc.) per il rendering del sito web, la visualizzazione sarà diversa da come era all’origine, poiché per tali elementi non vengono conservate precedenti versioni nell’archivio.

>[!CAUTION]
>
>Timewarp è uno strumento utile per aiutare gli autori a comprendere e creare i propri contenuti. Non deve essere utilizzato come registro di controllo o per fini legali.
