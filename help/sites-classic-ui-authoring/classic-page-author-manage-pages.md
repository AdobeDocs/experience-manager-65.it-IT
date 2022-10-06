---
title: Creazione e organizzazione delle pagine
seo-title: Creating and Organizing Pages
description: Questa sezione illustra come creare e gestire pagine in AEM, per poi creare contenuti su di esse.
seo-description: This section describes how to create and manage pages with AEM so that you can then create content on those pages.
uuid: 47ce137a-7a85-4b79-b4e0-fdf08a9e77bd
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 14b8758b-f164-429a-b299-33b0703f8bec
exl-id: bd2636d1-6f13-4c6c-b8cd-3bed9e83a101
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 88%

---

# Creazione e organizzazione delle pagine{#creating-and-organizing-pages}

Questa sezione illustra come creare e gestire pagine in Adobe Experience Manager (AEM), per poi [creare contenuti](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md) su di esse.

>[!NOTE]
>
>Il tuo account necessita dei [diritti di accesso](/help/sites-administering/security.md) e delle [autorizzazioni](/help/sites-administering/security.md#permissions) adeguati per intervenire sulle pagine, ad esempio per creare, copiare, spostare, modificare, eliminare elementi.
>
>Nell’eventualità di problemi, rivolgiti al tuo amministratore di sistema.

## Organizzazione del sito web {#organizing-your-website}

In qualità di autore dovrai organizzare il sito Web in AEM. Questo richiede che vengano create e denominate delle pagine di contenuto affinché:

* possiate trovare facilmente tali pagine nell’ambiente di authoring;
* i visitatori possano facilmente sfogliare le pagine nell’ambiente di pubblicazione.

È inoltre possibile utilizzare le [cartelle](#creating-a-new-folder) per organizzare i contenuti.

La struttura di un sito Web può essere pensata come una *struttura ad albero* che include le pagine di contenuti. I nomi di queste pagine di contenuti vengono utilizzati per formare gli URL, mentre il titolo è visualizzato alla visualizzazione del contenuto della pagina.

Di seguito è riportato un estratto del sito Geometrixx in cui, a titolo di esempio, verrà eseguito l’accesso alla pagina `Triangle`:

* Ambiente di authoring

   `http://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

* Ambiente di pubblicazione

   `http://localhost:4503/content/geometrixx/en/products/triangle.html`

   A seconda della configurazione dell’istanza, utilizza `/content` potrebbe essere facoltativo nell’ambiente di pubblicazione.

```xml
  /content
    /geometrixx
      /en
        /toolbar...
        /products
          /triangle
            /overview
            /features
          /square...
          /circle...
          /...
        /...
      /fr...
      /de...
      /es...
      /...
    /...
```

Questa struttura può essere visualizzata dalla console Siti web , che consente di utilizzare per [naviga attraverso la struttura ad albero](/help/sites-classic-ui-authoring/author-env-basic-handling.md#main-pars-text-15).

![chlimage_1-151](assets/chlimage_1-151.png)

### Convenzioni di denominazione delle pagine {#page-naming-conventions}

Durante la creazione di una nuova pagina sono disponibili due campi chiave:

* **[Titolo](#title)**:

   * Viene mostrato all’utente nella console ed è disponibile sopra il contenuto della pagina durante la modifica.
   * Questo campo è obbligatorio.

* **[Nome](#name)**:

   * Viene utilizzato per generare l’URI.
   * L’input dell’utente per questo campo è opzionale. Se non viene specificato, il nome viene derivato dal titolo.

Quando si crea una nuova pagina, AEM [convalida il nome della pagina in base alle convenzioni](/help/sites-developing/naming-conventions.md) imposto da AEM e JCR.

L’implementazione e l’elenco dei caratteri consentiti variano leggermente a seconda dell’interfaccia utente (è più esteso per l’interfaccia touch), ma il minimo consentito è:

* da “a” a “z”
* da “A” a “Z”
* da “0” a “9”
* _ (trattino basso)
* `-` (trattino/segno meno)

Utilizza esclusivamente questi caratteri se vuoi essere sicuro che vengano accettati e utilizzati (per informazioni complete sui caratteri consentiti, consulta le [convenzioni di denominazione](/help/sites-developing/naming-conventions.md)).

#### Titolo {#title}

Se specifichi solo il **titolo** della pagina quando crei una nuova pagina, AEM ne deriva il **nome** [da questa stringa e lo convalida in base alle convenzioni imposte da AEM e JCR. ](/help/sites-developing/naming-conventions.md) In entrambe le interfacce, un campo **Titolo** che contiene caratteri non validi viene accettato, ma tali caratteri vengono sostituiti nel nome derivato dal titolo. Ad esempio:

| Titolo | Nome derivato |
|---|---|
| Schön | schoen.html |
| SC%&amp;&amp;ast;ç+ | sc---c-.html |

#### Nome {#name}

Se specifichi il **nome** della pagina quando crei una nuova pagina, AEM lo [convalida in base alle convenzioni](/help/sites-developing/naming-conventions.md) imposte da AEM e JCR.

Nell’interfaccia classica, **impossibile immettere caratteri non validi** in **Nome** campo .

>[!NOTE]
>Nell’interfaccia touch è possibile: **impossibile inviare caratteri non validi** in **Nome** campo . Quando AEM rileva i caratteri non validi, il campo viene evidenziato e un messaggio di avviso segnala i caratteri che devono essere rimossi o sostituiti.

>[!NOTE]
>
>È consigliabile evitare di utilizzare codici di due lettere, come specificato dallo standard ISO-639-1, a meno che non si tratti dell’identificativo della lingua.
>
>Per ulteriori informazioni, consulta l’argomento relativo alla [preparazione dei contenuti per la traduzione](/help/sites-administering/tc-prep.md).

### Modelli {#templates}

In AEM, un modello specifica un particolare tipo di pagina e funge da base per la creazione di nuove pagine.

Il modello definisce la struttura di una pagina, inclusa un’immagine miniatura e altre proprietà. Ad esempio, potrai disporre di modelli separati per le pagine di prodotto, le sitemap e le informazioni di contatto. I modelli sono costituiti da [componenti](#components).

Con AEM vengono forniti diversi modelli. I modelli disponibili dipendono dal singolo sito Web e le informazioni da fornire (per la creazione di nuove pagine) dipendono dall’interfaccia in uso. I campi chiave sono i seguenti:

* **Titolo**
Il titolo visualizzato nella pagina web risultante.

* **Nome**
Utilizzato per la denominazione della pagina.

* **Modello**
Elenco di modelli disponibili per la generazione della nuova pagina.

### Componenti {#components}

I componenti sono gli elementi forniti da AEM che consentono di aggiungere specifici tipi di contenuto. AEM è dotato di una serie di componenti pronti all’uso che offrono funzionalità complete; tra cui:

* Testo
* Immagine
* Presentazione
* Video
* e molti altri.

Dopo aver creato e aperto una pagina è possibile [aggiungere contenuti utilizzando i componenti](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#insertinganewparagraph), disponibile dal [barra laterale](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick).

## Gestione delle pagine {#managing-pages}

### Creazione di una nuova pagina {#creating-a-new-page}

A meno che non siano state precedentemente create tutte le pagine necessarie, prima di iniziare a creare il contenuto è necessario creare una pagina:

1. Nella console **Siti Web** seleziona il livello al quale desideri creare la nuova pagina.

   Nell’esempio seguente viene creata una pagina al livello **Prodotti**, visualizzato nel riquadro di sinistra. Nel riquadro di destra sono visualizzate le pagine già presenti al livello **Prodotti**.

   ![screen_shot_2012-02-15at114413am](assets/screen_shot_2012-02-15at114413am.png)

1. Seleziona **Nuova pagina** nel menu **Nuovo** (fai clic sulla freccia accanto a **Nuovo**). Viene visualizzata la finestra **Crea pagina**.

   Fai clic sul menu **Nuovo** per accedere direttamente all’opzione **Nuova pagina**.

1. Nella finestra di dialogo **Crea pagina** effettua le seguenti operazioni:

   * Specifica un **Titolo** da mostrare all’utente.
   * Specifica un **Nome**, che verrà utilizzato per generare l’URI. Se non viene specificato, il nome viene derivato dal titolo.

      * Se specifichi il **nome** della pagina quando crei una nuova pagina, AEM [lo convalida in base alle convenzioni](/help/sites-developing/naming-conventions.md) imposte da AEM e JCR.
      * Nell’interfaccia classica **non è possibile immettere caratteri non validi** nel campo **Nome**.
   * Fate clic sul modello da utilizzare per creare la nuova pagina.

      Tale modello viene utilizzato come base per la nuova pagina, ad esempio per determinare il layout di base di una pagina di contenuto.
   >[!NOTE]
   >
   >Consulta [Convenzioni di denominazione delle pagine](#page-naming-conventions).

   Per creare una nuova pagina è necessario specificare almeno il **Titolo** e il modello richiesto.

   ![screen_shot_2012-02-15at114845am](assets/screen_shot_2012-02-15at114845am.png)

   >[!NOTE]
   >
   >Se desideri usare caratteri Unicode negli URL, imposta la proprietà Alias (`sling:alias`) ([proprietà Pagina](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)).

1. Fai clic su **Crea** per creare la pagina. Viene nuovamente visualizzata la console **Siti Web**, che ora contiene una voce per la nuova pagina.

   La console fornisce informazioni sulla pagina (ad esempio l’autore e la data dell’ultima modifica), che vengono aggiornate come necessario.

   >[!NOTE]
   >
   >È inoltre possibile creare una pagina mentre si modifica una pagina esistente. Utilizzo di **Crea pagina figlia **dal **Pagina** crea una nuova pagina direttamente sotto la pagina in corso di modifica.

### Apertura di una pagina per la modifica {#opening-a-page-for-editing}

Per aprire la pagina [da modificare](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#editing-a-component-content-and-properties) sono disponibili vari metodi:

* Nella console **Siti Web** fai **doppio clic** sulla voce relativa alla pagina per aprirla in modalità di modifica.

* Nella console **Siti Web** fate **clic con il pulsante destro del mouse** sull’elemento pagina e scegliete **Apri** dal menu di scelta rapida.

* Dopo avere aperto una pagina, fai clic sui collegamenti ipertestuali per accedere ad altre pagine del sito e modificarle.

### Copiare e incollare una pagina    {#copying-and-pasting-a-page}

La funzione di copia consente di copiare:

* Una singola pagina
* Una pagina con tutte le relative sottopagine

1. Nella console **Siti Web** seleziona la pagina da copiare.

   >[!NOTE]
   >
   >In questa fase non c’è differenza tra la copia di una singola pagina e la copia di una pagina con tutte le relative sottopagine.

1. Fate clic su **Copia**.

1. Passate alla nuova posizione e fate clic su:

   * **Incolla**, per incollare la pagina con tutte le relative sottopagine
   * **Maiusc+Incolla**, per incollare solo la pagina selezionata

   La pagina o le pagine vengono incollate nella nuova posizione.

   >[!NOTE]
   >
   >Se è già presente una pagina con lo stesso nome, il nome della pagina copiata viene modificato automaticamente.

   >[!NOTE]
   >
   >Puoi anche usare **Copia pagina** dalla scheda **Pagina** della barra laterale. Viene aperta una finestra di dialogo in cui puoi specificare la destinazione ecc.

### Spostamento o ridenominazione di una pagina {#moving-or-renaming-page}

>[!NOTE]
>
>Quando si rinomina una pagina, occorre rispettare le [convenzioni di denominazione delle pagine](#page-naming-conventions).

La procedura consente sia di spostare che di rinominare la pagina. La stessa procedura consente di effettuare le seguenti operazioni:

* Spostare una pagina in un nuovo percorso
* Rinominare una pagina mantenendola nello stesso percorso
* Spostare una pagina in un nuovo percorso e rinominarla

In AEM è disponibile una funzionalità che consente di aggiornare i collegamenti interni alla pagina rinominata o spostata. L’operazione può essere eseguita a livello di singola pagina, per assicurare la massima flessibilità.

Per spostare o rinominare una pagina:

1. Lo spostamento può essere effettuato tramite diversi metodi:

   * Nella console **Siti Web** fate clic per selezionare la pagina, quindi selezionate **Sposta**.
   * Nella console **Siti Web** puoi inoltre selezionare l’elemento di pagina, quindi fare **clic con il pulsante destro del mouse** e scegliere **Sposta**
   * Mentre modifichi una pagina puoi selezionare **Sposta pagina** dalla scheda **Pagina** della barra laterale.

1. Viene visualizzata la finestra **Sposta**, in cui è possibile specificare una nuova posizione, un nuovo nome per la pagina o entrambi.

   ![screen_shot_2012-02-15at121336pm](assets/screen_shot_2012-02-15at121336pm.png)

   Vengono inoltre elencate tutte le pagine che fanno riferimento alla pagina da spostare. A seconda della pagina che contiene il riferimento, può essere possibile modificare direttamente tali collegamenti e/o ripubblicare la pagina.

1. Compila i seguenti campi:

   * **Destinazione**

      Usate la mappa del sito (disponibile dal selettore a discesa) per selezionare la posizione in cui spostare la pagina.

      Se desiderate solo rinominare la pagina, ignorate questo campo.

   * **Sposta**

      Specificate la pagina da spostare. In genere questo campo viene precompilato per impostazione predefinita, a seconda di come e dove è stata avviata l’operazione di spostamento.

   * **Rinomina in**

      Per impostazione predefinita viene visualizzata l’etichetta della pagina corrente. Se necessario, specificate la nuova etichetta della pagina.

   * **Regola**

      Nelle pagine elencate, vengono aggiornati i collegamenti che puntano alla pagina spostata. Se ad esempio la pagina A include collegamenti alla pagina B, quando si sposta la pagina B AEM modifica automaticamente i collegamenti presenti nella pagina A.

      Questa casella di controllo può essere selezionata o deselezionata per ogni singola pagina contenente il riferimento.

   * **Ripubblica**

      Ripubblica la pagina che contiene il riferimento. Anche questa opzione può essere selezionata per ogni singola pagina.
   >[!NOTE]
   >
   >Se la pagina era già stata attivata, lo spostamento ne determina automaticamente la disattivazione. Per impostazione predefinita, viene riattivato al termine dello spostamento, ma questo può essere modificato deselezionando la **Ripubblica** per la pagina nel **Sposta** finestra.

1. Fai clic su **Sposta**. Verrà richiesto di confermare l’operazione. Fai clic su **OK** per confermare.

   >[!NOTE]
   >
   >Il titolo della pagina non verrà aggiornato.

### Eliminazione di una pagina {#deleting-a-page}

1. Per eliminare una pagina è possibile procedere in vari modi:

   * Nella console **Siti Web** fai clic per selezionare la pagina, quindi fai clic con il pulsante destro del mouse e scegli **Elimina** dal menu visualizzato.
   * Nella console **Siti Web** fai clic per selezionare la pagina, quindi seleziona **Elimina** dal menu della barra degli strumenti.
   * Nella barra laterale utilizza la scheda **Pagina** per selezionare **Elimina pagina**. La pagina attualmente aperta viene eliminata.

1. Poiché l’operazione non può essere annullata, dopo aver scelto di eliminare la pagina è necessario confermare la richiesta.

   >[!NOTE]
   >
   >Dopo l’eliminazione, se la pagina è stata pubblicata è possibile ripristinarne l’ultima versione o una versione specifica. Tuttavia, se erano state apportate ulteriori modifiche, la versione ripristinata potrebbe non avere esattamente lo stesso contenuto dell’ultima. Per ulteriori informazioni, consulta [Come ripristinare le pagine](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoringpages).

>[!NOTE]
>
>Se una pagina è già stata attivata, viene automaticamente disattivata prima dell’eliminazione.

### Blocco di una pagina   {#locking-a-page}

È possibile [bloccare/sbloccare una pagina](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#locking-a-page) da una console o quando si modifica una singola pagina. L’indicazione relativa al fatto che una pagina sia bloccata o meno è visualizzata in entrambe le posizioni.

### Creazione di una nuova cartella {#creating-a-new-folder}

>[!NOTE]
>
>Anche quando si rinomina una cartella occorre rispettare le [convenzioni di denominazione delle pagine](#page-naming-conventions).

1. Apri la console **Siti Web** e passa alla posizione desiderata.
1. In **Nuovo...** (fai clic sulla freccia accanto a **Nuovo...**), seleziona **Nuova cartella...**.
1. Verrà visualizzata la finestra di dialogo **Crea cartella**. Qui è possibile specificare il **Nome** e il **Titolo**:

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. Seleziona **Crea** per creare la nuova cartella.
