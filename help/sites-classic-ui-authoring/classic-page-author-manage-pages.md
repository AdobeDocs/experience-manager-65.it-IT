---
title: Creazione e organizzazione delle pagine
description: Questa sezione descrive come creare e gestire le pagine con AEM per poi creare contenuti su di esse.
uuid: 47ce137a-7a85-4b79-b4e0-fdf08a9e77bd
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 14b8758b-f164-429a-b299-33b0703f8bec
exl-id: bd2636d1-6f13-4c6c-b8cd-3bed9e83a101
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 14%

---

# Creazione e organizzazione delle pagine{#creating-and-organizing-pages}

Questa sezione descrive come creare e gestire le pagine con Adobe Experience Manager (AEM) in modo da poter [creare contenuto](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md) su quelle pagine.

>[!NOTE]
>
>Il tuo account deve [diritti di accesso appropriati](/help/sites-administering/security.md) e [permissions](/help/sites-administering/security.md#permissions) per intervenire sulle pagine, ad esempio per creare, copiare, spostare, modificare, eliminare elementi.
>
>Nell’eventualità di problemi, rivolgiti al tuo amministratore di sistema.

## Organizzazione del sito web {#organizing-your-website}

In qualità di autore dovrai organizzare il tuo sito web all’interno di AEM. Ciò comporta la creazione e la denominazione delle pagine di contenuto in modo che:

* sono facilmente reperibili nell’ambiente di authoring
* i visitatori del sito possono facilmente sfogliare le pagine nell’ambiente di pubblicazione

È inoltre possibile utilizzare le [cartelle](#creating-a-new-folder) per organizzare i contenuti.

La struttura di un sito web può essere pensata come *struttura ad albero* che contiene le pagine di contenuto. I nomi di queste pagine di contenuto vengono utilizzati per formare gli URL, mentre il titolo viene visualizzato quando viene visualizzato il contenuto della pagina.

di seguito è riportato un estratto del sito di Geometrixx; dove, ad esempio, il `Triangle` è accessibile la pagina:

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

* da &quot;a&quot; a &quot;z&quot;
* Da &quot;A&quot; a &quot;Z&quot;
* da &quot;0&quot; a &quot;9&quot;
* _ (trattino basso)
* `-` (trattino/segno meno)

Utilizza solo questi caratteri se vuoi essere sicuro che vengano accettati e utilizzati (per informazioni complete su tutti i caratteri consentiti, consulta [le convenzioni di denominazione](/help/sites-developing/naming-conventions.md)).

#### Titolo {#title}

Se specifichi solo il **titolo** della pagina quando crei una nuova pagina, AEM ne deriva il **nome** [da questa stringa e lo convalida in base alle convenzioni imposte da AEM e JCR. ](/help/sites-developing/naming-conventions.md) In entrambe le interfacce **Titolo** Il campo contenente caratteri non validi viene accettato, ma i caratteri non validi vengono sostituiti nel nome derivato dal campo. Ad esempio:

| Titolo | Nome derivato |
|---|---|
| Schön | schoen.html |
| SC%&amp;&amp;ast;ç+ | sc---c-.html |

#### Nome {#name}

Se specifichi il **nome** della pagina quando crei una nuova pagina, AEM lo [convalida in base alle convenzioni](/help/sites-developing/naming-conventions.md) imposte da AEM e JCR.

Nell’interfaccia classica, **impossibile immettere caratteri non validi** in **Nome** campo .

>[!NOTE]
>Nell’interfaccia touch è possibile: **impossibile inviare caratteri non validi** in **Nome** campo . Quando AEM rileva caratteri non validi, il campo viene evidenziato e viene visualizzato un messaggio di avviso che indica i caratteri che devono essere rimossi o sostituiti.

>[!NOTE]
>
>È consigliabile evitare di utilizzare un codice a due lettere come definito dallo standard ISO-639-1, a meno che non si tratti di una radice linguistica.
>
>Vedi [Preparazione del contenuto per la traduzione](/help/sites-administering/tc-prep.md) per ulteriori informazioni.

### Modelli {#templates}

In AEM, un modello specifica un tipo di pagina specializzato. Un modello viene utilizzato come base per la creazione di nuove pagine.

Il modello definisce la struttura di una pagina; inclusa un&#39;immagine in miniatura e altre proprietà. Ad esempio, puoi disporre di modelli separati per le pagine di prodotto, le mappe dei siti e le informazioni di contatto. I modelli sono formati da [componenti](#components).

AEM viene fornito con diversi modelli preconfigurati. I modelli disponibili dipendono dal singolo sito web e le informazioni da fornire (per la creazione di una nuova pagina) dipendono dall’interfaccia in uso. I campi chiave sono i seguenti:

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
* molti altri

Dopo aver creato e aperto una pagina è possibile [aggiungere contenuti utilizzando i componenti](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#insertinganewparagraph), disponibile dal [barra laterale](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick).

## Gestione delle pagine {#managing-pages}

### Creazione di una nuova pagina {#creating-a-new-page}

A meno che non siano state create tutte le pagine in anticipo, prima di iniziare a creare il contenuto devi creare una pagina:

1. Da **Siti Web** seleziona il livello in cui desideri creare una nuova pagina.

   Nell’esempio seguente viene creata una pagina sotto il livello **Prodotti** - nel riquadro a sinistra; il riquadro a destra mostra le pagine già presenti al livello sotto **Prodotti**.

   ![screen_shot_2012-02-15at114413am](assets/screen_shot_2012-02-15at114413am.png)

1. In **Nuovo...** (fai clic sulla freccia accanto a **Nuovo...**), seleziona **Nuova pagina...**. La **Crea pagina** si apre la finestra.

   Clic **Nuovo...** agisce anche come una scorciatoia **Nuova pagina...** opzione .

1. La **Crea pagina** consente di:

   * Fornisci un **Titolo**; viene visualizzato all’utente.
   * Fornisci un **Nome**; viene utilizzato per generare l’URI. Se non viene specificato, il nome verrà derivato dal titolo.

      * Se fornisci una pagina **Nome** quando si crea una nuova pagina, AEM [convalida il nome in base alle convenzioni](/help/sites-developing/naming-conventions.md) imposto da AEM e JCR.
      * Nell’interfaccia classica, **impossibile immettere caratteri non validi** in **Nome** campo .
   * Fai clic sul modello da utilizzare per creare la nuova pagina.

      Il modello viene utilizzato come base per la nuova pagina; ad esempio, per determinare il layout di base di una pagina di contenuto.
   >[!NOTE]
   >
   >Vedi [Convenzioni di denominazione delle pagine](#page-naming-conventions).

   Le informazioni minime necessarie per creare una nuova pagina sono le seguenti: **Titolo** e il modello richiesto.

   ![screen_shot_2012-02-15at114845am](assets/screen_shot_2012-02-15at114845am.png)

   >[!NOTE]
   >
   >Se desideri utilizzare caratteri unicode negli URL, imposta l’alias ( `sling:alias`), proprietà ([proprietà pagina](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)).

1. Fai clic su **Crea** per creare la pagina. Torna alla pagina **Siti Web** console che consente di visualizzare una voce per la nuova pagina.

   La console fornisce informazioni sulla pagina (ad esempio l’autore e la data dell’ultima modifica), che vengono aggiornate come necessario.

   >[!NOTE]
   >
   >Puoi anche creare una pagina mentre modifichi una pagina esistente. Utilizzo di **Crea pagina figlia **dal **Pagina** crea una nuova pagina direttamente sotto la pagina in corso di modifica.

### Apertura di una pagina per la modifica {#opening-a-page-for-editing}

È possibile aprire la pagina [modificato](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#editing-a-component-content-and-properties) con uno dei vari metodi:

* Da **Siti Web** console **doppio clic** la voce della pagina per aprirla in modalità di modifica.

* Da **Siti Web** console **fare clic con il pulsante destro del mouse** (menu di scelta rapida) l’elemento di pagina, quindi seleziona **Apri** dal menu.

* Dopo aver aperto una pagina, fai clic sui collegamenti ipertestuali per passare ad altre pagine del sito e modificarle.

### Copiare e incollare una pagina    {#copying-and-pasting-a-page}

Durante la copia, puoi copiare:

* una singola pagina
* una pagina con tutte le relative sottopagine

1. Da **Siti Web** seleziona la pagina da copiare.

   >[!NOTE]
   >
   >A questo punto, è irrilevante se si desidera copiare una singola pagina o le pagine secondarie sottostanti.

1. Fai clic su **Copia**.

1. Passa alla nuova posizione e fai clic su:

   * **Incolla** - per incollare la pagina con tutte le relative sottopagine
   * **Maiusc+Incolla** - per incollare solo la pagina selezionata

   Le pagine vengono incollate nella nuova posizione.

   >[!NOTE]
   >
   >Se una pagina esistente ha già lo stesso nome, il nome della pagina può essere modificato automaticamente.

   >[!NOTE]
   >
   >È inoltre possibile utilizzare **Copia pagina** dal **Pagina** scheda della barra laterale. Viene visualizzata una finestra di dialogo in cui puoi specificare la destinazione e così via.

### Spostamento o ridenominazione di una pagina {#moving-or-renaming-page}

>[!NOTE]
>
>Anche la ridenominazione di una pagina è soggetta alla [Convenzioni di denominazione delle pagine](#page-naming-conventions) quando si specifica il nuovo nome della pagina.

La procedura per spostare o rinominare una pagina è la stessa. Con la stessa azione puoi:

* spostare una pagina in un nuovo percorso
* rinominare una pagina nella stessa posizione
* spostare una pagina in un nuovo percorso e rinominarla

AEM offre la funzionalità di aggiornare i collegamenti interni alla pagina rinominata o spostata. Questa operazione può essere eseguita pagina per pagina per garantire la massima flessibilità.

Per spostare o rinominare una pagina:

1. Esistono diversi metodi per attivare uno spostamento:

   * Da **Siti Web** console, fai clic su per selezionare la pagina, quindi seleziona **Sposta...**
   * Da **Siti Web** è inoltre possibile selezionare l’elemento pagina, quindi **fare clic con il pulsante destro del mouse** e seleziona **Sposta...**
   * Durante la modifica di una pagina è possibile selezionare **Sposta pagina** dal **Pagina** scheda della barra laterale.

1. La **Sposta** finestre aperte; qui puoi specificare una nuova posizione, un nuovo nome per la pagina o entrambi.

   ![screen_shot_2012-02-15at121336pm](assets/screen_shot_2012-02-15at121336pm.png)

   Vengono inoltre elencate tutte le pagine che fanno riferimento alla pagina da spostare. A seconda dello stato della pagina di riferimento, è possibile modificare tali collegamenti sulle pagine e/o ripubblicarli.

1. Compila i campi seguenti, a seconda dei casi:

   * **Destinazione**

      Utilizza la mappa del sito (disponibile dal selettore a discesa) per selezionare il percorso in cui spostare la pagina.

      Se la pagina viene rinominata, ignora questo campo.

   * **Sposta**

      Specifica la pagina da spostare. In genere questo campo viene precompilato per impostazione predefinita, a seconda di come e dove è stata avviata l’azione di spostamento.

   * **Rinomina in**

      Per impostazione predefinita viene visualizzata l’etichetta della pagina corrente. Specifica la nuova etichetta di pagina, se necessario.

   * **Regola**

      Aggiorna i collegamenti nella pagina elencata che puntano alla pagina spostata: ad esempio, se la pagina A include collegamenti alla pagina B, AEM regola i collegamenti nella pagina A nel caso in cui si sposti la pagina B.

      Questa opzione può essere selezionata/deselezionata per ogni singola pagina contenente un riferimento.

   * **Ripubblica**

      Ripubblica la pagina di riferimento; anche questa opzione può essere selezionata per ogni singola pagina.
   >[!NOTE]
   >
   >Se la pagina era già stata attivata, lo spostamento la disattiverà automaticamente. Per impostazione predefinita, viene riattivato al termine dello spostamento, ma questo può essere modificato deselezionando la **Ripubblica** per la pagina nel **Sposta** finestra.

1. Fai clic su **Sposta**. Sarà richiesta la conferma. Fai clic su **OK** per confermare.

   >[!NOTE]
   >
   >Il titolo della pagina non viene aggiornato.

### Eliminazione di una pagina {#deleting-a-page}

1. È possibile eliminare una pagina da diverse posizioni:

   * All&#39;interno di **Siti Web** console, fai clic per selezionare la pagina, quindi fai clic con il pulsante destro del mouse e seleziona **Elimina** dal menu risultante.
   * All&#39;interno di **Siti Web** console, fai clic su per selezionare la pagina, quindi seleziona **Elimina** dal menu della barra degli strumenti.
   * Nella barra laterale utilizza la **Pagina** scheda da selezionare **Elimina pagina** : consente di eliminare la pagina attualmente aperta.

1. Dopo aver selezionato di eliminare una pagina è necessario confermare la richiesta, poiché l’azione non può essere annullata.

   >[!NOTE]
   >
   >Dopo l’eliminazione, se la pagina è stata pubblicata è possibile ripristinare l’ultima versione (o una versione specifica), ma questo potrebbe non avere esattamente lo stesso contenuto dell’ultima versione se sono state apportate ulteriori modifiche. Vedi [Come ripristinare le pagine](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoringpages) per ulteriori dettagli.

>[!NOTE]
>
>Se una pagina è già stata attivata, verrà automaticamente disattivata prima dell’eliminazione.

### Blocco di una pagina   {#locking-a-page}

È possibile [bloccare/sbloccare una pagina](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#locking-a-page) da una console o quando si modifica una singola pagina. L’indicazione relativa al fatto che una pagina sia bloccata o meno è visualizzata in entrambe le posizioni.

### Creazione di una nuova cartella {#creating-a-new-folder}

>[!NOTE]
>
>Anche le cartelle sono soggette al [Convenzioni di denominazione delle pagine](#page-naming-conventions) quando si specifica il nuovo nome della cartella.

1. Apri **Siti Web** e passa alla posizione desiderata.
1. In **Nuovo...** (fai clic sulla freccia accanto a **Nuovo...**), seleziona **Nuova cartella...**.
1. La **Crea cartella** si aprirà la finestra di dialogo . Nella finestra puoi immettere il **Nome** e il **Titolo**:

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. Seleziona **Crea** per creare la nuova cartella.
