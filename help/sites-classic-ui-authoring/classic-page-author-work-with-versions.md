---
title: Utilizzo delle versioni di pagina
description: Il controllo delle versioni crea uno "snapshot" di una pagina in un momento specifico.
uuid: 06e112cd-e4ae-4ee0-882d-7009f53ac85b
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 48936115-4be2-4b0c-81ce-d61e43e4535d
docset: aem65
exl-id: 4eb0de5e-0306-4166-9cee-1297a5cd14ce
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 22%

---

# Utilizzo delle versioni di una pagina  {#working-with-page-versions}

Il controllo delle versioni crea uno &quot;snapshot&quot; di una pagina in un momento specifico. Con il controllo delle versioni è possibile eseguire le seguenti operazioni:

* Crea una versione di una pagina.
* Ripristinare una versione precedente di una pagina per annullare, ad esempio, una modifica apportata a una pagina.
* Confronta la versione corrente di una pagina con una versione precedente con le differenze nel testo e nelle immagini evidenziate.

## Creazione di una nuova versione   {#creating-a-new-version}

Per creare una nuova versione di una pagina:

1. Nel browser, apri la pagina per la quale desideri creare una nuova versione.
1. Nella barra laterale, seleziona la **Controllo delle versioni** , quindi la **Crea versione** sottoscheda .

   ![screen_shot_2012-02-14at40259pm](assets/screen_shot_2012-02-14at40259pm.png)

1. Inserisci un **Commento** (facoltativo).
1. Per impostare un’etichetta per la versione (facoltativa), fai clic sul pulsante **Altro >>** e impostare **Etichetta** per assegnare un nome alla versione. Se l’etichetta non è impostata, la versione è un numero incrementato automaticamente.
1. Fai clic su **Crea versione**. Sulla pagina viene visualizzato un messaggio in grigio; ad esempio: La versione 1.2 creata per: Camicie.

>[!NOTE]
>
>Una versione viene creata automaticamente quando la pagina viene attivata.

## Ripristino di una versione di pagina dalla barra laterale {#restoring-a-page-version-from-sidekick}

Per ripristinare una versione precedente della pagina:

1. Apri la pagina di cui desideri ripristinare una versione precedente.
1. Nella barra laterale, seleziona la **Controllo delle versioni** , quindi la **Ripristina versione** sottoscheda .

   ![screen_shot_2012-02-14at42949pm](assets/screen_shot_2012-02-14at42949pm.png)

1. Seleziona la versione da ripristinare e seleziona **Ripristina**.

## Ripristino di una versione della pagina dalla console {#restoring-a-page-version-from-the-console}

Questo metodo può essere utilizzato per ripristinare una versione di una pagina. Può essere utilizzato anche per ripristinare le pagine precedentemente eliminate:

1. In **Siti Web** console, passa alla pagina da ripristinare e selezionala.
1. Dal menu principale seleziona **Strumenti**, quindi **Ripristina**:

   ![screen_shot_2012-02-08at41326pm](assets/screen_shot_2012-02-08at41326pm.png)

1. Selezione **Ripristina versione..** elenca le versioni dei documenti presenti nella cartella corrente. Anche se una pagina è stata eliminata, viene elencata l’ultima versione:

   ![screen_shot_2012-02-08at45743pm](assets/screen_shot_2012-02-08at45743pm.png)

1. Seleziona la versione da ripristinare e fai clic su **Ripristina**. AEM ripristina le versioni o gli alberi selezionati.

### Ripristino di una struttura ad albero dalla console {#restoring-a-tree-from-the-console}

Questo metodo può essere utilizzato per ripristinare una versione di una pagina. Può essere utilizzato anche per ripristinare le pagine precedentemente eliminate:

1. In **Siti Web** console, individua la cartella da ripristinare e selezionala.
1. Dal menu principale seleziona **Strumenti**, quindi **Ripristina**.
1. Selezione **Ripristina albero..** apre la finestra di dialogo per selezionare la struttura ad albero da ripristinare:

   ![screen_shot_2012-02-08at45743pm-1](assets/screen_shot_2012-02-08at45743pm-1.png)

1. Fai clic su **Ripristina**. AEM ripristina la struttura ad albero selezionata.

## Confronto con una versione precedente {#comparing-with-a-previous-version}

Per confrontare la versione corrente della pagina con una versione precedente:

1. Nel browser, apri la pagina da confrontare con una versione precedente.
1. Nella barra laterale, seleziona la **Controllo delle versioni** , quindi la **Ripristina versione** n sottoscheda.

   ![screen_shot_2012-02-14at42949pm-1](assets/screen_shot_2012-02-14at42949pm-1.png)

1. Seleziona la versione da confrontare e fai clic sul pulsante **Differenze** pulsante .
1. Le differenze tra la versione corrente e quella selezionata vengono visualizzate come segue:

   * Il testo eliminato è rosso ed è barrato.
   * Il testo aggiunto è evidenziato in verde.
   * Le immagini aggiunte o eliminate sono contrassegnate in verde.

   ![chlimage_1-75](assets/chlimage_1-75.png)

1. Nella barra laterale, seleziona la **Ripristina versione** sottoscheda e fai clic su **&lt;&lt;back span=&quot;&quot; id=&quot;3&quot; translate=&quot;no&quot; /> per visualizzare la versione corrente.**

## Timewarp   {#timewarp}

Timewarp è una funzione progettata per simulare lo stato ***di pubblicazione*** di una pagina in specifici momenti nel passato.

Lo scopo è quello di consentire di tenere traccia del sito web pubblicato in un determinato momento. Questo utilizza le attivazioni di pagina per determinare lo stato dell’ambiente di pubblicazione.

Per effettuare questo collegamento:

* Il sistema cerca la versione della pagina che era attiva al momento selezionato.
* In altre parole, la versione mostrata era stata creata/attivata *prima* del momento temporale selezionato in Timewarp.
* Quando si passa a una pagina che è stata eliminata, questa viene riprodotta purché nella directory archivio siano ancora disponibili le versioni precedenti della pagina.
* Se non viene trovata alcuna versione pubblicata, Timewarp ripristina lo stato corrente della pagina nell’ambiente di authoring (in modo da evitare un errore 404 di pagina non trovata, che impedirebbe di continuare la navigazione).

>[!NOTE]
>
>Se dalla directory archivio sono state rimosse delle versioni, Timewarp non può mostrare la visualizzazione corretta. Inoltre, se sono stati modificati alcuni elementi (come codice, css, immagini ecc.) per il rendering del sito web, la visualizzazione sarà diversa da come era all’origine, in quanto per tali elementi non vengono conservate precedenti versioni nell’archivio.

### Utilizzo del calendario Timewarp {#using-the-timewarp-calendar}

Timewarp è disponibile dalla barra laterale.

La versione Calendario viene utilizzata per visualizzare un giorno specifico:

1. Apri **Controllo delle versioni** , quindi fai clic su **Timewarp** (vicino alla parte inferiore della barra laterale). Viene visualizzata la seguente finestra di dialogo:

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. Utilizzando i selettori data e ora, specifica la data/ora desiderata e fai clic su **Vai**.

   Timewarp visualizza la pagina così come era nel suo stato di pubblicazione prima o alla data scelta.

   >[!NOTE]
   >
   >Timewarp funziona correttamente solo se la pagina è stata precedentemente pubblicata. In caso contrario viene mostrata la pagina corrente nell’ambiente di authoring.

   >[!NOTE]
   >
   >Se passi a una pagina che è stata rimossa o eliminata dall’archivio, questa verrà riprodotta correttamente se nell’archivio sono ancora disponibili versioni precedenti della pagina.

   >[!NOTE]
   >
   >Non è possibile modificare la versione precedente della pagina. ma solo visualizzarla. Se desideri ripristinare la versione precedente, devi farlo manualmente utilizzando la funzione di [ripristino](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoring-a-page-version-from-sidekick).

1. Al termine della visualizzazione della pagina, fai clic su:

   * **Esci da Timewarp** per uscire e tornare alla pagina corrente di authoring.
   * [Mostra timeline](#using-the-timewarp-timeline) per visualizzare la timeline.

   ![chlimage_1-77](assets/chlimage_1-77.png)

### Utilizzo della timeline Timewarp {#using-the-timewarp-timeline}

La versione timeline consente di visualizzare una panoramica delle attività di pubblicazione presenti nella pagina.

Per visualizzare la timeline del documento:

1. Per visualizzare la timeline potete effettuare le seguenti operazioni:

   1. Apri **Controllo delle versioni** , quindi fai clic su **Timewarp** (vicino alla parte inferiore della barra laterale).

   1. Usa la finestra di dialogo della barra laterale visualizzata dopo [utilizzo del calendario Timewarp](#using-the-timewarp-calendar).

1. Fai clic su **Mostra timeline** - verrà visualizzata la timeline del documento; ad esempio:

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. Seleziona e sposta (trascina) la timeline per spostarti all’interno della timeline del documento.

   * Tutte le righe indicano le versioni pubblicate.
Quando una pagina viene attivata, inizia una nuova riga. Ogni volta che il documento viene modificato viene visualizzato un nuovo colore.
Nell’esempio seguente, la linea rossa indica che la pagina è stata modificata durante l’intervallo di tempo della versione iniziale verde e la linea gialla indica che la pagina è stata modificata in un secondo momento durante la versione rossa, ecc.

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. Clic:

   1. **Vai** per visualizzare il contenuto della pagina pubblicata nel momento in cui è selezionata.
   1. Quando visualizzi il contenuto, utilizza **Esci da Timewarp** per uscire e tornare alla pagina corrente di authoring.

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
