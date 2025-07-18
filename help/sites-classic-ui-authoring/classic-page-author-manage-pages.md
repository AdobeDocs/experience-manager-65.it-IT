---
title: Creazione e organizzazione delle pagine
description: Questa sezione descrive come creare e gestire le pagine con AEM in modo da poter poi creare contenuti su di esse.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: bd2636d1-6f13-4c6c-b8cd-3bed9e83a101
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 25bf0d64b6839afec0112ea8c9fde0510e56ccf4
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 16%

---

# Creazione e organizzazione delle pagine{#creating-and-organizing-pages}

Questa sezione descrive come creare e gestire le pagine con Adobe Experience Manager (AEM) in modo da poter [creare contenuto](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md) su tali pagine.

>[!NOTE]
>
>Il tuo account necessita dei [diritti di accesso appropriati](/help/sites-administering/security.md) e delle [autorizzazioni](/help/sites-administering/security.md#permissions) per intervenire sulle pagine, ad esempio per creare, copiare, spostare, modificare, eliminare.
>
>Nell’eventualità di problemi, rivolgiti al tuo amministratore di sistema.

## Organizzazione del sito web {#organizing-your-website}

In qualità di autore, devi organizzare il tuo sito web all’interno di AEM. A tale scopo, dovrai creare e denominare le pagine di contenuto affinché:

* si trovano facilmente nell’ambiente di authoring
* i visitatori del sito possono facilmente sfogliarli nell’ambiente di pubblicazione

È inoltre possibile utilizzare le [cartelle](#creating-a-new-folder) per organizzare i contenuti.

La struttura di un sito Web può essere considerata come una *struttura ad albero* che contiene le pagine di contenuto. I nomi di queste pagine di contenuto vengono utilizzati per formare gli URL, mentre il titolo viene visualizzato quando viene visualizzato il contenuto della pagina.

Di seguito è riportato un estratto dal sito Geometrixx, dove, ad esempio, sarà possibile accedere alla pagina `Triangle`:

* Ambiente di authoring

  `http://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

* Ambiente di pubblicazione

  `http://localhost:4503/content/geometrixx/en/products/triangle.html`

  A seconda della configurazione dell&#39;istanza, l&#39;utilizzo di `/content` potrebbe essere facoltativo nell&#39;ambiente di pubblicazione.

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

Questa struttura può essere visualizzata dalla console Siti Web, che è possibile utilizzare per [spostarsi nella struttura ad albero](/help/sites-classic-ui-authoring/author-env-basic-handling.md#main-pars-text-15).

![chlimage_1-151](assets/chlimage_1-151.png)

### Convenzioni di denominazione delle pagine {#page-naming-conventions}

Durante la creazione di una pagina sono disponibili due campi chiave:

* **[Titolo](#title)**:

   * Viene mostrato all’utente nella console ed è disponibile sopra il contenuto della pagina durante la modifica.
   * Questo campo è obbligatorio.

* **[Nome](#name)**:

   * Viene utilizzato per generare l’URI.
   * L’input dell’utente per questo campo è opzionale. Se non viene specificato, il nome viene derivato dal titolo.

Durante la creazione di una pagina, AEM [convalida il nome della pagina in base alle convenzioni](/help/sites-developing/naming-conventions.md) imposte da AEM e JCR.

L’implementazione e l’elenco dei caratteri consentiti varia leggermente a seconda dell’interfaccia utente (è più esteso per l’interfaccia touch), ma il minimo consentito è:

* Da &#39;a&#39; a &#39;z&#39;
* Da &#39;A&#39; a &#39;Z&#39;
* Da &#39;0&#39; a &#39;9&#39;
* _ (trattino basso)
* `-` (trattino/segno meno)

Utilizzare solo questi caratteri per essere certi che vengano accettati o utilizzati (se sono necessari dettagli completi di tutti i caratteri consentiti, vedere [le convenzioni di denominazione](/help/sites-developing/naming-conventions.md)).

#### Titolo {#title}

Se durante la creazione di una pagina si specifica solo una pagina **Titolo**, AEM deriva la pagina **Nome** da questa stringa e [convalida il nome in base alle convenzioni](/help/sites-developing/naming-conventions.md) imposte da AEM e JCR. In entrambe le interfacce verrà accettato un campo **Titolo** contenente caratteri non validi, ma al nome derivato verranno sostituiti i caratteri non validi. Ad esempio:

| Titolo | Nome derivato |
|---|---|
| Schön | schoen.html |
| SC%&amp;&ast;ç+ | sc---c-.html |

#### Nome {#name}

Se durante la creazione di una pagina si specifica **Nome**, AEM [convalida il nome in base alle convenzioni](/help/sites-developing/naming-conventions.md) imposte da AEM e JCR.

Nell&#39;interfaccia classica **non è possibile immettere caratteri non validi** nel campo **Nome**.

>[!NOTE]
>Nell&#39;interfaccia utente touch **non è possibile inviare caratteri non validi** nel campo **Name**. Quando AEM rileva caratteri non validi, il campo viene evidenziato e viene visualizzato un messaggio esplicativo per indicare i caratteri da rimuovere o sostituire.

>[!NOTE]
>
>È consigliabile evitare di utilizzare un codice a due lettere come definito dallo standard ISO-639-1, a meno che non si tratti di una directory principale della lingua.
>
>Per ulteriori informazioni, consulta l’argomento relativo alla [preparazione dei contenuti per la traduzione](/help/sites-administering/tc-prep.md).

### Modelli {#templates}

In AEM, un modello specifica un tipo di pagina particolare. Un modello viene utilizzato come base per qualsiasi nuova pagina creata.

Il modello definisce la struttura di una pagina, incluse un’immagine di miniatura e altre proprietà. Ad esempio, puoi usare modelli distinti per pagine di prodotti, sitemap e informazioni di contatto. I modelli sono costituiti da [componenti](#components).

AEM viene fornito con diversi modelli preconfigurati. I modelli disponibili dipendono dal singolo sito Web e le informazioni da fornire (al momento della creazione della nuova pagina) dipendono dall’interfaccia utente utilizzata. I campi chiave sono i seguenti:

* **Titolo**
Il titolo visualizzato nella pagina web risultante.

* **Nome**
Utilizzato per la denominazione della pagina.

* **Modello**
Elenco di modelli disponibili per la generazione della nuova pagina.

### Componenti {#components}

I componenti sono gli elementi forniti da AEM che consentono di aggiungere specifici tipi di contenuto. AEM viene fornito con una serie di componenti pronti all’uso che offrono funzionalità complete, tra cui:

* Testo
* Immagine
* Presentazione
* Video
* molti altri

Dopo aver creato e aperto una pagina, puoi [aggiungere contenuto utilizzando i componenti](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#insertinganewparagraph), disponibili nella [barra laterale](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick).

## Gestione delle pagine {#managing-pages}

### Creazione di una nuova pagina {#creating-a-new-page}

A meno che non siano state create tutte le pagine in anticipo, prima di poter iniziare a creare il contenuto devi creare una pagina:

1. Dalla console **Siti Web**, selezionare il livello in cui si desidera creare una pagina.

   Nell&#39;esempio seguente si sta creando una pagina al livello **Prodotti**, visualizzato nel riquadro sinistro. Nel riquadro destro vengono visualizzate le pagine già esistenti al livello in **Prodotti**.

   ![schermata_shot_2012-02-15at114413am](assets/screen_shot_2012-02-15at114413am.png)

1. Nel menu **Nuovo...** (fare clic sulla freccia accanto a **Nuovo...**), selezionare **Nuova pagina...**. Viene visualizzata la finestra **Crea pagina**.

   Facendo clic su **Nuova...** si può accedere anche all&#39;opzione **Nuova pagina...**.

1. La finestra di dialogo **Crea pagina** consente di:

   * Fornisci un **Titolo** da mostrare all&#39;utente.
   * Fornisci un **Nome**; viene utilizzato per generare l&#39;URI. Se non viene specificato, il nome verrà derivato dal titolo.

      * Se durante la creazione di una pagina si specifica **Nome**, AEM [convalida il nome in base alle convenzioni](/help/sites-developing/naming-conventions.md) imposte da AEM e JCR.
      * Nell&#39;interfaccia classica **non è possibile immettere caratteri non validi** nel campo **Nome**.

   * Fare clic sul modello da utilizzare per creare la nuova pagina.

     Il modello viene utilizzato come base per la nuova pagina, ad esempio per determinare il layout di base di una pagina di contenuto.

   >[!NOTE]
   >
   >Consulta [Convenzioni di denominazione delle pagine](#page-naming-conventions).

   Le informazioni minime necessarie per creare una pagina sono il **Titolo** e il modello richiesto.

   ![schermata_shot_2012-02-15at114845am](assets/screen_shot_2012-02-15at114845am.png)

   >[!NOTE]
   >
   >Se si desidera utilizzare caratteri Unicode negli URL, impostare la proprietà Alias (`sling:alias`) ([proprietà pagina](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)).

1. Fai clic su **Crea** per creare la pagina. Torna alla console **Siti Web** dove puoi visualizzare una voce per la nuova pagina.

   La console fornisce informazioni sulla pagina (ad esempio, quando è stata modificata l’ultima volta e da chi) che viene aggiornata, se necessario.

   >[!NOTE]
   >
   >È inoltre possibile creare una pagina quando si modifica una pagina esistente. Utilizzando **Crea pagina secondaria** dalla scheda **Pagina** della barra laterale, viene creata una pagina direttamente sotto la pagina in fase di modifica.

### Apertura di una pagina per la modifica {#opening-a-page-for-editing}

Puoi aprire la pagina da [modificare](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#editing-a-component-content-and-properties) con uno dei seguenti metodi:

* Dalla console **Siti Web**, puoi **fare doppio clic** sulla voce della pagina per aprirla per la modifica.

* Dalla console **Siti Web**, puoi **fare clic con il pulsante destro del mouse** (menu di scelta rapida) sull&#39;elemento della pagina, quindi selezionare **Apri** dal menu.

* Dopo aver aperto una pagina, è possibile passare ad altre pagine del sito (per modificarle) facendo clic sui collegamenti ipertestuali.

### Copiare e incollare una pagina    {#copying-and-pasting-a-page}

Durante la copia, puoi copiare:

* una singola pagina
* una pagina con tutte le relative pagine secondarie

1. Dalla console **Siti Web**, selezionare la pagina da copiare.

   >[!NOTE]
   >
   >In questa fase, è irrilevante se si desidera copiare una singola pagina o le relative sottopagine.

1. Fai clic su **Copia**.

1. Passa alla nuova posizione e fai clic su:

   * **Incolla**: per incollare la pagina con tutte le pagine secondarie
   * **Maiusc + Incolla** - per incollare solo la pagina selezionata

   Le pagine vengono incollate nella nuova posizione.

   >[!NOTE]
   >
   >Il nome della pagina può essere regolato automaticamente se una pagina esistente ha già lo stesso nome.

   >[!NOTE]
   >
   >Puoi anche utilizzare **Copia pagina** dalla scheda **Pagina** della barra laterale. Viene visualizzata una finestra di dialogo in cui è possibile specificare la destinazione e così via.

### Spostamento o ridenominazione di una pagina {#moving-or-renaming-page}

>[!NOTE]
>
>La ridenominazione di una pagina è inoltre soggetta a [Convenzioni di denominazione delle pagine](#page-naming-conventions) quando si specifica il nuovo nome della pagina.

La procedura per spostare o rinominare una pagina è la stessa. Con la stessa azione puoi:

* spostare una pagina in una nuova posizione
* rinominare una pagina nella stessa posizione
* spostare una pagina in una nuova posizione e rinominarla contemporaneamente

AEM offre la funzionalità di aggiornamento dei collegamenti interni alla pagina rinominata o spostata. Questa operazione può essere eseguita a livello di singola pagina, per assicurare la massima flessibilità.

Per spostare o rinominare una pagina:

1. Esistono diversi metodi per attivare uno spostamento:

   * Dalla console **Siti Web**, fare clic per selezionare la pagina, quindi selezionare **Sposta...**
   * Dalla console **Siti Web**, puoi anche selezionare l&#39;elemento della pagina, quindi **fai clic con il pulsante destro del mouse** e seleziona **Sposta...**
   * Quando modifichi una pagina puoi selezionare **Sposta pagina** dalla scheda **Pagina** della barra laterale.

1. Viene visualizzata la finestra **Sposta** in cui è possibile specificare una nuova posizione, un nuovo nome per la pagina o entrambi.

   ![schermata_shot_2012-02-15at121336pm](assets/screen_shot_2012-02-15at121336pm.png)

   Nella pagina sono inoltre elencate tutte le pagine che fanno riferimento direttamente o indirettamente alla pagina spostata. A seconda dello stato della pagina di riferimento, è possibile regolare tali collegamenti e/o ripubblicare le pagine.

1. Compila i campi seguenti, a seconda dei casi:

   * **Destinazione**

     Utilizza la mappa del sito (disponibile tramite il selettore a discesa) per selezionare il percorso in cui spostare la pagina.

     Se rinomini solo la pagina, ignora questo campo.

   * **Sposta**

     Specifica la pagina da spostare: in genere viene compilata per impostazione predefinita, a seconda di come e dove hai avviato l’azione di spostamento.

   * **Rinomina in**

     L&#39;etichetta della pagina corrente viene visualizzata per impostazione predefinita. Se necessario, specifica la nuova etichetta della pagina.

   * **Regola**

     Aggiorna i collegamenti nella pagina elencata che puntano alla pagina spostata: ad esempio, se la pagina A contiene collegamenti alla pagina B, AEM regola i collegamenti nella pagina A in caso di spostamento della pagina B.

     Può essere selezionato/deselezionato per ogni singola pagina di riferimento.

   * **Ripubblica**

     Ripubblica la pagina di riferimento; anche in questo caso è possibile selezionarla per ogni singola pagina.

   >[!NOTE]
   >
   >Se la pagina è già stata attivata, lo spostamento la disattiverà automaticamente. Per impostazione predefinita, verrà riattivato al termine dello spostamento, ma questo comportamento può essere modificato deselezionando il campo **Ripubblica** per la pagina nella finestra **Sposta**.

1. Fare clic su **Sposta**. Sarà necessaria la conferma. Fai clic su **OK** per confermare.

   >[!NOTE]
   >
   >Il titolo della pagina non verrà aggiornato.

### Eliminazione di una pagina {#deleting-a-page}

1. Puoi eliminare una pagina da varie posizioni:

   * Nella console **Siti Web**, fare clic per selezionare la pagina, quindi fare clic con il pulsante destro del mouse e selezionare **Elimina** dal menu risultante.
   * Nella console **Siti Web**, fare clic per selezionare la pagina, quindi selezionare **Elimina** dal menu della barra degli strumenti.
   * Nella barra laterale utilizzare la scheda **Pagina** per selezionare **Elimina pagina**, eliminando la pagina attualmente aperta.

1. Dopo aver selezionato di eliminare una pagina, è necessario confermare la richiesta, in quanto l’azione non può essere annullata.

   >[!NOTE]
   >
   >Dopo l’eliminazione, se la pagina è stata pubblicata è possibile ripristinare la versione più recente (o specifica), ma questo potrebbe non avere esattamente lo stesso contenuto dell’ultima versione se sono state apportate ulteriori modifiche. Per ulteriori dettagli, vedere [Come ripristinare le pagine](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoringpages).

>[!NOTE]
>
>Se una pagina è già attivata, verrà automaticamente disattivata prima dell’eliminazione.

### Blocco di una pagina   {#locking-a-page}

È possibile [bloccare/sbloccare una pagina](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#locking-a-page) da una console o durante la modifica di una singola pagina. Le informazioni sulle pagine bloccate vengono visualizzate anche in entrambe le posizioni.

### Creazione di una nuova cartella {#creating-a-new-folder}

>[!NOTE]
>
>Le cartelle sono inoltre soggette a [Convenzioni di denominazione delle pagine](#page-naming-conventions) quando si specifica il nome della nuova cartella.

1. Apri la console **Siti Web** e passa alla posizione desiderata.
1. Nel menu **Nuovo...** (fare clic sulla freccia accanto a **Nuovo...**), selezionare **Nuova cartella...**.
1. Viene visualizzata la finestra di dialogo **Crea cartella**. Nella finestra puoi immettere il **Nome** e il **Titolo**:

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. Seleziona **Crea** per creare la nuova cartella.
