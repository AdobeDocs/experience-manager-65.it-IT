---
title: Utilizzare la modalità Layout per ridimensionare i componenti per la comunicazione interattiva
description: 'Definire la posizione dei componenti utilizzando la griglia reattiva disponibile in modalità Layout '
feature: Interactive Communication
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---


# Utilizzare la modalità Layout per ridimensionare i componenti {#use-layout-mode-to-resize-components}

L’interfaccia di creazione del canale web di comunicazione interattiva consente di ridimensionare i componenti utilizzando la modalità Layout . Trascina i punti blu all’interno delle colonne per definire i punti iniziale e finale per posizionare i componenti. I punti blu vengono visualizzati dopo aver toccato il componente all’interno della griglia reattiva. La griglia reattiva è costituita da 12 colonne uguali. L’ombreggiatura del colore bianco e blu nelle colonne alternative differenzia una colonna dall’altra.

È possibile utilizzare la modalità Layout per ridimensionare i componenti per tutti i tipi di dispositivi, ad esempio desktop, tablet, telefoni e altri dispositivi più piccoli. Il tablet deriva automaticamente la configurazione del layout dalla versione desktop e i dispositivi più piccoli derivano la configurazione del layout dal telefono. Tuttavia, è possibile ignorare le configurazioni derivate automaticamente per definire una configurazione diversa per ogni tipo di dispositivo.

>[!NOTE]
>
>Se si sta creando il canale Web utilizzando [Canale di stampa come master](../../forms/using/create-interactive-communication.md) per una comunicazione interattiva, i componenti disponibili per il ridimensionamento includono anche i sottomoduli e i campi generati automaticamente nel canale Web utilizzando il canale Stampa. Il canale Web mantiene il layout degli elementi del canale Stampa in modalità Layout.

## Modalità Layout di accesso {#access-layout-mode}

Seleziona **Layout** dall’elenco a discesa visualizzato nella parte superiore dell’interfaccia di authoring delle comunicazioni interattive accanto all’opzione **Anteprima**. Il modulo viene visualizzato in modalità Layout .

1. Accedi all&#39;istanza di authoring AEM e passa a **Adobe Experience Manager** > **Forms** > **Forms &amp; Documents**.
1. Crea una nuova o apri una [Comunicazione interattiva](../../forms/using/create-interactive-communication.md) esistente.
1. Seleziona **Layout** dall&#39;elenco a discesa che viene visualizzato nella parte superiore accanto all&#39;opzione **Anteprima**. Il modulo viene visualizzato in modalità Layout .

   ![Modalità Layout per le comunicazioni interattive](assets/layout_mode_ic_new.png)

## Ridimensiona i componenti {#resize-components}

1. In modalità Layout, tocca il componente da ridimensionare. I punti blu vengono visualizzati all’inizio e alla fine della griglia reattiva.
1. Trascina i punti blu per definire la posizione del componente nella griglia reattiva.

   ![Ridimensionamento utilizzando la modalità Layout](assets/layout_mode_resize_new_updated.png)

   La barra degli strumenti visualizzata dopo aver toccato i componenti è costituita dalle seguenti opzioni:

   * **Elemento padre:** seleziona l’elemento principale di un componente.
   * **Mobile in nuova riga:** sposta il componente sulla riga successiva se sono presenti più componenti nella stessa riga.

   È possibile annullare tutte le modifiche di ridimensionamento e applicare il layout predefinito al pannello contenente i componenti ridimensionati utilizzando l’opzione **[!UICONTROL Ripristina layout punto di interruzione]** ( ![Ripristina punto di interruzione](assets/reverttopreviouslypublishedversion.png)). Toccare l’elemento padre del componente ridimensionato per visualizzare l’opzione .

   >[!NOTE]
   >
   >Non è possibile ridimensionare la colonna di una tabella, la barra degli strumenti, il pulsante della barra degli strumenti e i componenti dell’area di destinazione utilizzando la modalità Layout. Utilizza la modalità Stile per ridimensionare questi componenti.

### Esempio {#example}

**Obiettivo:** inserire un componente tabella e un componente immagine e posizionarli paralleli tra loro in una comunicazione interattiva.

1. Inserire i componenti tabella e immagine utilizzando la modalità Modifica nel canale Web di una comunicazione interattiva. Il componente Immagine viene visualizzato dopo il componente Tabella.
1. Passa alla modalità Layout e tocca il componente Tabella . I punti blu per ridimensionare il componente vengono visualizzati nelle colonne 1 e 12.
1. Trascina il punto blu nella colonna 12 alla colonna 6 della griglia reattiva.

   ![Definire il punto finale della tabella](assets/layout_mode_end_point_table_new.png)

1. Allo stesso modo, seleziona il componente Immagine e trascina il punto blu nella colonna 1 alla colonna 7 della griglia reattiva. I componenti tabella e immagine vengono visualizzati in parallelo.

   ![Tabella e immagine in parallelo in modalità Layout](assets/table_image_parallel_new.png)

   Puoi selezionare il componente Immagine e toccare l’opzione **Mobile in nuova riga** disponibile nella barra degli strumenti per spostare il componente Immagine sulla riga successiva.

## Ridimensiona i pannelli {#resize-panels-layout-mode}

Per ridimensionare l’intero pannello invece dei singoli componenti, esegui i seguenti passaggi:

1. Tocca uno dei componenti del pannello da ridimensionare, seleziona ![Seleziona elemento padre](assets/select_parent_icon.svg) e seleziona la prima opzione nell’elenco a discesa, se il pannello è l’elemento padre diretto del componente.

   I punti blu vengono visualizzati all’inizio e alla fine della griglia reattiva.

1. Trascina i punti blu per definire la posizione del pannello nella griglia reattiva.
È possibile ripetere i passaggi 1 e 2 e selezionare ![Seleziona padre](assets/float_to_new_line_icon.svg) per spostare il pannello ridimensionato alla riga successiva.

## Definire il layout a più colonne per un pannello

Esegui i seguenti passaggi per definire il numero di colonne per un pannello:

1. In modalità **[!UICONTROL Modifica]**, tocca il pannello, seleziona ![Configura](assets/configure_icon.png) e seleziona **[!UICONTROL Reattivo - tutto ciò che si trova sulla pagina senza navigazione]** dall’elenco a discesa **[!UICONTROL Layout del pannello]**.

1. Tocca ![Salva](assets/save_icon.svg) per salvare le proprietà.

1. In modalità **[!UICONTROL Layout]**, tocca uno dei componenti del pannello, seleziona ![Seleziona padre](assets/select_parent_icon.svg) e seleziona il pannello.

1. Tocca ![più colonne](assets/multi-column.svg) e seleziona il numero di colonne dall’elenco a discesa. Il numero di colonne può variare da 1 a 12. Il pannello viene diviso in un layout a più colonne.

![in modalità layout a più colonne](assets/multi-column-layout.png)

## Disattiva la modalità Layout per i moduli con layout reattivo precedente {#disable-layout-mode-for-forms-with-old-responsive-layout}

È possibile disattivare la modalità Layout per i moduli con layout reattivo precedente modificando le proprietà del modello utilizzato nel modulo.

Esegui i seguenti passaggi per disabilitare la modalità Layout :

1. Seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Modelli]** e apri il modello utilizzato nel modulo in modalità **[!UICONTROL Modifica]**.
1. Seleziona il Contenitore documento nel riquadro a sinistra e tocca **[!UICONTROL Criterio.]**

   ![Disattiva modalità Layout](assets/policy_disable_layout_mode.png)

1. Tocca la scheda **[!UICONTROL Impostazioni layout]** e seleziona **[!UICONTROL Disattiva modalità layout]**.
1. Tocca ![Salva modifiche](assets/save_icon.png) per salvare le proprietà del modello.

