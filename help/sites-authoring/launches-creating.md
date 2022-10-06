---
title: Creazione dei lanci
seo-title: Creating Launches
description: Puoi creare un lancio per abilitare l’aggiornamento di una nuova versione di pagine web esistenti da attivare in futuro.
seo-description: You can create a launch to enable the updating of a new version of existing web pages for future activation.
uuid: c1a32710-8189-4a2e-bf2f-428ab30d48c8
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 4ec6b408-a165-4617-8d90-e89d8a415bb3
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: bc7897da-15f6-4de4-a9fd-9dd84e6c7eed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 98%

---

# Creazione dei lanci{#creating-launches}

Puoi creare un lancio per abilitare l’aggiornamento di una nuova versione di pagine web esistenti da attivare in futuro. Per creare un lancio, è necessario specificare un titolo e la pagina di origine:

* Il titolo viene visualizzato nella barra [Riferimenti](/help/sites-authoring/author-environment-tools.md#references), dalla quale gli autori potranno accedere per lavorarci.
* Per impostazione predefinita nel lancio vengono incluse le pagine figlie della pagina di origine. Se necessario, potete comunque usare anche solo la pagina sorgente.
* Per impostazione predefinita, [Live Copy](/help/sites-administering/msm.md) aggiorna automaticamente le pagine di lancio mano a mano che vengono modificate le pagine sorgente. Per evitare che vengano apportate tali modifiche automatiche, puoi specificare che venga creata una copia statica.

Facoltativamente, puoi specificare la **Data lancio** (e l’ora) per definire quando promuovere e attivare le pagine del lancio. Tuttavia, la **Data lancio** funziona solo in combinazione con il flag **Production Ready** (vedi la sezione [Modifica di una configurazione di lancio](/help/sites-authoring/launches-editing.md#editing-a-launch-configuration)). Affinché le azioni vengano effettivamente eseguite in automatico, è necessario impostare entrambe.

## Creazione di un lancio {#creating-a-launch}

Puoi creare un lancio da Sites o dalla console Lanci:

1. Apri la console **Sites** o **Lanci**.

   >[!NOTE]
   >
   >Quando usi la console **Sites** solitamente si accede alla posizione della pagina sorgente, ma non è obbligatorio, perché puoi accedervi quando selezioni l’**Origine del lancio** nella procedura guidata.

1. A seconda della console utilizzata:

   * **Lanci**:

      1. Seleziona **Crea lancio** dalla barra degli strumenti per aprire la procedura guidata.
   * **Sites**:

      1. Seleziona **Crea** nella barra degli strumenti per aprire la casella di selezione.
      1. Da qui seleziona **Crea lancio** per aprire la procedura guidata.

   >[!NOTE]
   >
   >Nella console **Sites** è inoltre possibile utilizzare la [modalità di selezione](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources) per scegliere una pagina prima di fare clic su **Crea**.
   >
   >La pagina selezionata verrà così utilizzata come pagina sorgente iniziale.

1. Nel passaggio **Seleziona origine** è necessario usare la funzione **Aggiungi pagine**. Puoi selezionare più pagine, specificando il percorso per ciascuna:

   * Passa alla posizione desiderata.
   * Seleziona le pagine sorgente e conferma (segno di spunta).

   Ripeti in base alle esigenze.  

   ![chlimage_1-225](assets/chlimage_1-225.png)

   >[!NOTE]
   >
   >Per aggiungere pagine e/o rami a un lancio, questi devono essere all’interno di un sito; in altre parole, in una directory comune di primo livello.
   >
   >Se un sito contiene directory principali per lingue inferiori al primo livello, le pagine e i rami di un lancio devono essere in una directory principale per lingua comune.

1. Per ogni voce puoi specificare le seguenti opzioni:

   * **Includi le pagine secondarie**:

      * Specifica se creare il lancio con o senza pagine figlie.  Per impostazione predefinita, le pagine secondarie sono incluse.

   Procedi con **Successivo**.

   ![chlimage_1-226](assets/chlimage_1-226.png)

1. Nel passaggio **Proprietà** della procedura guidata puoi specificare:

   * **Titolo lancio**: nome del lancio. Scegli un nome che possa essere facilmente riconosciuto dagli autori.
   * **con contenuto esistente**: il contenuto originale verrà utilizzato per creare il lancio.
   * **con un nuovo modello per sostituire la pagina**: per ulteriori dettagli, vedi [Creare un lancio con un nuovo modello](#create-launch-with-new-template).
   * **Eredita i dati live della pagina di origine**: seleziona questa opzione per aggiornare automaticamente il contenuto delle pagine di lancio quando cambiano le pagine di origine. Questa opzione permette di ottenere questo risultato rendendo il lancio un [Live Copy](/help/sites-administering/msm.md).

      Per impostazione predefinita, questa opzione è selezionata.

   * **Data lancio**: la data e l&#39;ora in cui la copia del lancio deve essere attivata (in base alla segnalazione **Produzione pronta**; consulta [Lanci: l&#39;ordine degli eventi](/help/sites-authoring/launches.md#launches-the-order-of-events)).

   ![chlimage_1-227](assets/chlimage_1-227.png)

1. Tocca o fai clic su **Crea** per completare il processo e creare il nuovo lancio. La finestra di dialogo di conferma chiederà se desideri aprire il lancio immediatamente.

   Se torni alla console (con **Fine**), puoi visualizzare il lancio (e accedervi) in uno dei due modi seguenti:

   * Dalla [**** console Lanci](/help/sites-authoring/launches.md#the-launches-console)
   * da [**Riferimenti** nella console **Sites**](/help/sites-authoring/launches.md#launches-in-references-sites-console)

### Creare un lancio con un nuovo modello {#create-launch-with-new-template}

Quando [creai un lancio](/help/sites-authoring/launches-creating.md#create-launch-with-new-template) puoi utilizzare un nuovo modello scegliendo la seguente opzione:

**con un nuovo modello per sostituire la pagina**

>[!CAUTION]
>
>Questa opzione è disponibile solo quando crei un lancio dalla console **Sites**. Non è disponibile quando crei un lancio dalla console **Lanci**.

![chlimage_1-228](assets/chlimage_1-228.png)

Quando selezioni questa opzione:

* le altre opzioni disponibili vengono aggiornate,
* un nuovo passaggio permette di selezionare il modello desiderato.

![chlimage_1-229](assets/chlimage_1-229.png)

>[!CAUTION]
>
>Quando utilizzi un modello diverso, la nuova pagina sarà vuota. A causa della diversa struttura della pagina, non verrà copiato alcun contenuto.
>
>Questo metodo può essere utilizzato per modificare il modello di una [pagina esistente](/help/sites-authoring/managing-pages.md#creating-a-new-page); tuttavia, deve essere tenuta in considerazione la perdita di contenuto.

### Creazione di un lancio nidificato {#creating-a-nested-launch}

Un lancio nidificato (lancio all’interno di un altro lancio) dà la possibilità di creare un lancio da un lancio esistente in modo che gli autori possano sfruttare le modifiche già apportate, anziché doverle apportare più volte per ogni lancio.

>[!NOTE]
>
>Vedi anche [Promozione di un lancio nidificato](/help/sites-authoring/launches-promoting.md#promoting-a-nested-launch).

#### Creazione di un lancio nidificato: console Lanci {#creating-a-nested-launch-launches-console}

La creazione di un lancio nidificato dalla console **Lanci** è molto simile alla creazione di qualsiasi altra forma di lancio, con l’eccezione che è necessario passare al ramo dei lanci `/content/launches`:

1. Nella console **Lanci** seleziona **Crea**.
1. Fai clic su **Aggiungi pagine**, quindi specifica `/content/launches` nel filtro per individuare il ramo lanci. Scegli il lancio necessario e conferma con **Seleziona**:

   ![chlimage_1-230](assets/chlimage_1-230.png)

1. Procedi con **Successivo** e imposta le **Proprietà** come per un qualsiasi altro lancio.

   ![chlimage_1-231](assets/chlimage_1-231.png)

#### Creazione di un lancio nidificato: console Sites {#creating-a-nested-launch-sites-console}

Per creare un lancio nidificato dalla console **Sites**, basato su un lancio esistente:

1. Accedi a [Lancio da Riferimenti (console Sites)](/help/sites-authoring/launches.md#launches-in-references-sites-console) per visualizzare le azioni disponibili.
1. Seleziona **Crea lancio** per aprire la procedura guidata (poiché l’origine è già stata selezionata, ignorerà il passaggio **Seleziona origine**).

1. Immetti il **Titolo lancio** e tutti gli altri dettagli richiesti (come con un normale lancio).

1. Tocca o fai clic su **Crea** per completare il processo e creare il nuovo lancio. La finestra di dialogo di conferma chiederà se desideri aprire il lancio immediatamente.

   Se fai clic su **Fine**, vieni riportato alla barra **Riferimenti** della console **Sites**, se selezioni la pagina appropriata viene visualizzato il tuo nuovo lancio.

### Eliminazione di un lancio {#deleting-a-launch}

Puoi eliminare un lancio dalla [console Lanci](/help/sites-authoring/launches.md#the-launches-console):

* Seleziona il lancio, toccando o facendo clic sulla miniatura.
* Viene visualizzata la barra degli strumenti: scegli Elimina.
* Conferma l’azione.

>[!CAUTION]
>
>L’eliminazione del lancio rimuove il lancio stesso e tutti i lanci nidificati discendenti.
