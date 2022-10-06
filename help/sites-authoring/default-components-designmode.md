---
title: Configurazione dei componenti in modalità Progettazione
seo-title: Configuring Components in Design Mode
description: Configurazione dei componenti in modalità Progettazione
seo-description: null
uuid: b9c9792d-4398-446d-8767-44d4e7ce9a2e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 8ae6817a-16d3-4740-b67a-498e75adf350
exl-id: 5e232886-75c1-4f0f-b359-4739ae035fd3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 82%

---

# Configurazione dei componenti in modalità Progettazione{#configuring-components-in-design-mode}

Quando si installa un’istanza di AEM out-of-the-box, nel browser Componenti è immediatamente disponibile una serie di componenti.

Oltre a questi, sono disponibili anche vari altri componenti. È possibile utilizzare la modalità Progettazione per [attiva/disattiva tali componenti](#enable-disable-components). Quando è attivata e si trova sulla pagina, è possibile utilizzare la modalità Progettazione per [configurare gli aspetti della progettazione del componente](#configuring-the-design-of-a-component) modificando i parametri degli attributi.

>[!NOTE]
>
>Quando modifichi tali componenti, presta molta attenzione. Le impostazioni sono spesso una parte integrante della progettazione dell’intero sito Web e dovrebbero essere modificate solo da un utente con la necessaria esperienza e con le relative autorizzazioni, ad esempio un amministratore o sviluppatore. Per ulteriori informazioni, consulta [Sviluppo di componenti](/help/sites-developing/components.md).

>[!NOTE]
>
>La modalità Progettazione è disponibile solo per i modelli statici. I modelli creati con modelli modificabili devono essere modificati mediante l’[editor modelli](/help/sites-authoring/templates.md).

>[!NOTE]
>
>La modalità Progettazione è disponibile solo per le configurazioni del progetto memorizzate come contenuto sotto ( `/etc`).
>
>A partire da AEM 6.4, si consiglia di memorizzare le progettazioni come dati di configurazione in `/apps` per supportare scenari di distribuzione continui. Disegni immagazzinati in `/apps` non sono modificabili in fase di esecuzione e la modalità Progettazione non sarà disponibile agli utenti non amministratori per tali modelli.

Questo comporta l’aggiunta o la rimozione dei componenti consentiti nel sistema di paragrafi per la pagina. Anche il sistema di paragrafi (`parsys`) stesso è un componente, che contiene gli altri componenti paragrafo. Il sistema di paragrafi consente agli autori di aggiungere a una pagina componenti di tipi diversi e contiene tutti gli altri componenti paragrafo. Ciascun tipo di paragrafo è rappresentato da un componente.

Ad esempio, il contenuto di una pagina prodotto può contenere quanto segue:

* Un’immagine del prodotto (sotto forma di immagine o paragrafo testo e immagine)
* La descrizione del prodotto (come paragrafo testo)
* Una tabella con dati tecnici (come un paragrafo tabella)
* Un modulo che può essere compilato dagli utenti (come paragrafo inizio modulo, elemento modulo e fine modulo)

>[!NOTE]
>
>Per ulteriori informazioni su [](/help/sites-developing/components.md), consulta [Sviluppo di componenti](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) e `parsys`Linee guida per l’utilizzo di modelli e componenti.

>[!CAUTION]
>
>La modifica del design con la modalità Progettazione descritta in questo articolo rappresenta il metodo consigliato per definire i progetti dei modelli statici
>
>Ad esempio, la modifica dei progetti in CRX DE non è consigliata e l’applicazione di tali progetti può variare da un comportamento all’altro. Per ulteriori informazioni, consulta il documento per sviluppatori [Modelli di pagina - Statici](/help/sites-developing/page-templates-static.md#how-template-designs-are-applied).

## Attivare o disattivare componenti {#enable-disable-components}

Per attivare o disattivare un componente:

1. Seleziona la modalità **Progettazione**:

   ![screen_shot_2018-03-22at103113](assets/screen_shot_2018-03-22at103113.png)

1. Tocca o fai clic su un componente. Quando è selezionato, il componente è evidenziato da un bordo blu.

   ![screen_shot_2018-03-22at103204](assets/screen_shot_2018-03-22at103204.png)

1. Tocca o fai clic su **Elemento padre** icona.

   ![](do-not-localize/screen_shot_2018-03-22at103204.png)

   Viene selezionato il sistema di paragrafi contenente il componente corrente.

1. Nella barra delle azioni dell’elemento padre viene visualizzata l’icona **Configura**. 

   ![](do-not-localize/screen_shot_2018-03-22at103256.png)

   Selezionala per aprire la relativa finestra di dialogo.

1. Nella finestra di dialogo, definisci i componenti disponibili nel browser dei componenti durante la modifica della pagina corrente:

   ![screen_shot_2018-03-22at103329](assets/screen_shot_2018-03-22at103329.png)

   La finestra di dialogo contiene due schede:

   * Componenti consentiti
   * Impostazioni

   **Componenti consentiti**

   Sulla **Componenti consentiti** definisci quali componenti sono disponibili per parsys.

   * I componenti sono raggruppati in base ai gruppi di componenti, che possono essere espansi e ridotti.
   * Per selezionare tutti i componenti di un gruppo, attiva la casella del nome del gruppo; per deselezionare tutti i componenti di un gruppo, disattiva questa casella.
   * Se la casella contiene un meno (-) significa che è selezionato almeno un elemento del gruppo, ma non tutti.
   * È disponibile un sistema di ricerca per filtrare i componenti in base al nome.
   * Il numero a destra del nome di un gruppo di componenti indica quanti sono i componenti selezionati in tale gruppo, a prescindere dal filtro.

   Definisci la configurazione di ogni componente di pagina. Se le pagine figlie usano lo stesso modello e/o lo stesso componente di pagina (generalmente allineato), la stessa configurazione sarà applicata al sistema di paragrafi corrispondente.

   >[!NOTE]
   >
   >I componenti per modulo adattivo sono progettati per funzionare nel contenitore per moduli adattivo e sfruttare l’ecosistema Moduli. Di conseguenza, questi componenti devono essere utilizzati solo nell’editor di moduli adattivi e non funzionano nell’editor pagine dell’ambiente Sites.

   **Impostazioni**

   Nella scheda **Impostazioni** puoi definire opzioni aggiuntive, ad esempio per disegnare un ancoraggio per ciascun componente e definire il margine delle celle di ciascun contenitore.

1. Seleziona **Fine** per salvare la configurazione.

## Configurare l’aspetto di un componente {#configuring-the-design-of-a-component}

1. Seleziona la modalità **Progettazione**:

   ![screen_shot_2018-03-22at103113-1](assets/screen_shot_2018-03-22at103113-1.png)

1. Tocca o fai clic su un componente con bordo blu. In questo esempio è selezionato un componente immagine protagonista.

   ![screen_shot_2018-03-22at103434](assets/screen_shot_2018-03-22at103434.png)

1. Utilizza l’icona **Configura** per aprire la finestra di dialogo. 

   ![](do-not-localize/screen_shot_2018-03-22at103256-1.png)

   Nella finestra di dialogo Progettazione, puoi configurare il componente in base ai parametri di progettazione disponibili.

   ![screen_shot_2018-03-22at103530](assets/screen_shot_2018-03-22at103530.png)

   La finestra di dialogo contiene tre schede:

   * Principale
   * Funzioni
   * Stili

   **Proprietà**

   La scheda **Proprietà** consente di configurare i parametri di progettazione principali del componente. Ad esempio, per un componente immagine puoi definire la dimensione massima e minima consentita dell’immagine.

   **Funzioni**

   La scheda **Funzioni** consente di abilitare o disabilitare funzioni aggiuntive del componente. Ad esempio, per un componente immagine puoi definire l’orientamento, le opzioni di ritaglio disponibili e se un’immagine può essere caricata.

   **Stili**

   La scheda **Stili** consente di definire le classi CSS e gli stili da utilizzare con il componente.

   ![screen_shot_2018-03-22at103741](assets/screen_shot_2018-03-22at103741.png)

   Utilizza il pulsante **Aggiungi** per aggiungere altre voci a un elenco di più voci.

   ![chlimage_1-94](assets/chlimage_1-94.png)

   Utilizza l’icona** Elimina **per rimuovere una voce da un elenco di più voci.

   ![](do-not-localize/screen_shot_2018-03-22at103809.png)

   Utilizza l’icona **Sposta** per cambiare l’ordine delle voci in un elenco di più voci.

   ![](do-not-localize/screen_shot_2018-03-22at103816.png)

1. Tocca o fai clic sull’icona **Fine** per salvare e chiudere la finestra di dialogo.
