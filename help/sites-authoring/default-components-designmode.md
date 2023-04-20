---
title: Configurazione dei componenti predefiniti in modalità Progettazione
description: Configurazione dei componenti in modalità Progettazione
uuid: b9c9792d-4398-446d-8767-44d4e7ce9a2e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 8ae6817a-16d3-4740-b67a-498e75adf350
exl-id: 5e232886-75c1-4f0f-b359-4739ae035fd3
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 1%

---

# Configurazione dei componenti predefiniti in modalità Progettazione{#configuring-components-in-design-mode}

Quando AEM’istanza è installata out-of-the-box, nel browser Componenti è immediatamente disponibile una selezione di componenti.

Oltre a questi, sono disponibili anche vari altri componenti. È possibile utilizzare la modalità Progettazione per [attiva/disattiva tali componenti](#enable-disable-components). Quando è attivata e si trova sulla pagina, è possibile utilizzare la modalità Progettazione per [configurare gli aspetti della progettazione del componente](#configuring-the-design-of-a-component) modificando i parametri degli attributi.

>[!NOTE]
>
>Presta attenzione quando modifichi questi componenti. Le impostazioni di progettazione sono spesso una parte integrante della progettazione dell’intero sito web e dovrebbero quindi essere modificate solo da un utente con le autorizzazioni e l’esperienza appropriate, spesso da un amministratore o sviluppatore. Vedi [Sviluppo di componenti](/help/sites-developing/components.md) per ulteriori informazioni.

>[!NOTE]
>
>La modalità Progettazione è disponibile solo per i modelli statici. I modelli creati con modelli modificabili devono essere modificati utilizzando [editor modelli](/help/sites-authoring/templates.md).

>[!NOTE]
>
>La modalità Progettazione è disponibile solo per le configurazioni di progettazione memorizzate come contenuto in ( `/etc`).
>
>A partire da AEM 6.4, si consiglia di memorizzare le progettazioni come dati di configurazione in `/apps` per supportare scenari di distribuzione continui. Disegni immagazzinati in `/apps` non sono modificabili in fase di esecuzione e la modalità Progettazione non sarà disponibile agli utenti non amministratori per tali modelli.

Ciò comporta l’aggiunta o la rimozione dei componenti consentiti nel sistema di paragrafi per la pagina. Il sistema paragrafo ( `parsys`) è un componente composto che contiene tutti gli altri componenti paragrafo. Il sistema di paragrafi consente agli autori di aggiungere a una pagina componenti di tipi diversi e contiene tutti gli altri componenti paragrafo. Ciascun tipo di paragrafo è rappresentato da un componente.

Ad esempio, il contenuto di una pagina prodotto può contenere un sistema paragrafo contenente i seguenti elementi:

* Un’immagine del prodotto (sotto forma di un paragrafo immagine o testo)
* Descrizione del prodotto (come paragrafo di testo)
* Tabella con dati tecnici (come paragrafo di una tabella)
* Un modulo compilato dagli utenti (come paragrafo iniziale, elemento modulo e fine modulo)

>[!NOTE]
>
>Vedi [Sviluppo di componenti](/help/sites-developing/components.md) e [Linee guida per l’utilizzo di modelli e componenti](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) per ulteriori informazioni `parsys`.

>[!CAUTION]
>
>La modifica della progettazione con la modalità Progettazione descritta in questo articolo rappresenta il modo consigliato per definire le progettazioni dei modelli statici
>
>Ad esempio, la modifica dei progetti in CRX DE non è una best practice e l’applicazione di tali progetti può variare dal comportamento previsto. Consulta il documento per sviluppatori [Modelli di pagina - Statici](/help/sites-developing/page-templates-static.md#how-template-designs-are-applied) per ulteriori informazioni.

## Attivare/disattivare i componenti {#enable-disable-components}

Per attivare o disattivare un componente:

1. Seleziona la **Progettazione** modalità.

   ![screen_shot_2018-03-22at103113](assets/screen_shot_2018-03-22at103113.png)

1. Tocca o fai clic su un componente. Se selezionato, il componente avrà un bordo blu.

   ![screen_shot_2018-03-22at103204](assets/screen_shot_2018-03-22at103204.png)

1. Tocca o fai clic su **Elemento padre** icona.

   ![](do-not-localize/screen_shot_2018-03-22at103204.png)

   Viene selezionato il sistema di paragrafi contenente il componente corrente.

1. La **Configura** Nella barra delle azioni dell’elemento padre viene visualizzata l’icona relativa al sistema paragrafo.

   ![](do-not-localize/screen_shot_2018-03-22at103256.png)

   Selezionare questa opzione per visualizzare la finestra di dialogo.

1. Utilizza la finestra di dialogo per definire i componenti disponibili nel browser dei componenti durante la modifica della pagina corrente.

   ![screen_shot_2018-03-22at103329](assets/screen_shot_2018-03-22at103329.png)

   La finestra di dialogo presenta due schede:

   * Componenti consentiti
   * Impostazioni

   **Componenti consentiti**

   Sulla **Componenti consentiti** definisci quali componenti sono disponibili per parsys.

   * I componenti sono raggruppati in base ai gruppi di componenti, che possono essere espansi e compressi.
   * Per selezionare un intero gruppo, seleziona il nome del gruppo e deseleziona tutti gli elementi deselezionati deselezionando .
   * Un segno meno rappresenta almeno uno, ma non tutti gli elementi di un gruppo, selezionati.
   * È disponibile una ricerca per filtrare un componente per nome.
   * I conteggi elencati a destra del nome del gruppo di componenti rappresentano il numero totale di componenti selezionati in tali gruppi, indipendentemente dal filtro.

   Puoi definire la configurazione per componente pagina. Se le pagine figlie utilizzano lo stesso modello e/o lo stesso componente di pagina (generalmente allineato), la stessa configurazione verrà applicata al sistema di paragrafi corrispondente.

   >[!NOTE]
   >
   >I componenti per moduli adattivi sono progettati per funzionare all’interno del contenitore per moduli adattivi e sfruttare l’ecosistema Forms. Pertanto, questi componenti devono essere utilizzati solo nell’editor di moduli adattivi e non funzioneranno nell’editor di pagine Sites.

   **Impostazioni**

   Sulla **Impostazioni** è possibile definire opzioni aggiuntive, ad esempio per disegnare un ancoraggio per ciascun componente e definire la spaziatura delle celle di ciascun contenitore.

1. Seleziona **Fine** per salvare la configurazione.

## Configurazione della progettazione di un componente {#configuring-the-design-of-a-component}

1. Seleziona la **Progettazione** modalità.

   ![screen_shot_2018-03-22at103113-1](assets/screen_shot_2018-03-22at103113-1.png)

1. Tocca o fai clic su un componente con bordo blu. In questo esempio viene selezionato un componente immagine protagonista.

   ![screen_shot_2018-03-22at103434](assets/screen_shot_2018-03-22at103434.png)

1. Utilizza la **Configura** per aprire la finestra di dialogo.

   ![](do-not-localize/screen_shot_2018-03-22at103256-1.png)

   Nella finestra di dialogo Progettazione, puoi configurare il componente in base ai parametri di progettazione disponibili.

   ![screen_shot_2018-03-22at103530](assets/screen_shot_2018-03-22at103530.png)

   La finestra di dialogo presenta tre schede:

   * Principale
   * Funzioni
   * Stili

   **Proprietà**

   La **Proprietà** consente di configurare i parametri di progettazione importanti del componente. Ad esempio, per un componente immagine puoi definire la dimensione massima e minima consentita per l’immagine.

   **Funzioni**

   La **Funzioni** consente di abilitare o disabilitare funzioni aggiuntive del componente. Ad esempio, per un componente immagine puoi definire l’orientamento dell’immagine, le opzioni di ritaglio disponibili e se è possibile caricare un’immagine.

   **Stili**

   La **Stili** La scheda ti consente di definire le classi e gli stili CSS da utilizzare con il componente.

   ![screen_shot_2018-03-22at103741](assets/screen_shot_2018-03-22at103741.png)

   Utilizza la **Aggiungi** per aggiungere ulteriori voci a un elenco di più voci.

   ![chlimage_1-94](assets/chlimage_1-94.png)

   Utilizza l’icona** Elimina **per rimuovere una voce da un elenco di più voci.

   ![](do-not-localize/screen_shot_2018-03-22at103809.png)

   Utilizza la **Sposta** per ridisporre l’ordine delle voci in un elenco a più voci.

   ![](do-not-localize/screen_shot_2018-03-22at103816.png)

1. Tocca o fai clic su **Fine** per salvare e chiudere la finestra di dialogo.
