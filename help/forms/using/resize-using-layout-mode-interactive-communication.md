---
title: Utilizzare la modalità Layout per ridimensionare i componenti per la comunicazione interattiva
description: Definire la posizione dei componenti utilizzando la griglia reattiva disponibile in modalità Layout
feature: Interactive Communication
exl-id: 9534fcb2-4260-4dd0-9f7e-779b10fd3a22
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 1%

---

# Utilizzare la modalità Layout per ridimensionare i componenti {#use-layout-mode-to-resize-components}

L’interfaccia di creazione del canale web di comunicazione interattiva consente di ridimensionare i componenti utilizzando la modalità Layout . Trascina i punti blu all’interno delle colonne per definire i punti iniziale e finale per posizionare i componenti. I punti blu vengono visualizzati dopo aver toccato il componente all’interno della griglia reattiva. La griglia reattiva è costituita da 12 colonne uguali. L’ombreggiatura del colore bianco e blu nelle colonne alternative differenzia una colonna dall’altra.

È possibile utilizzare la modalità Layout per ridimensionare i componenti per tutti i tipi di dispositivi, ad esempio desktop, tablet, telefoni e altri dispositivi più piccoli. Il tablet deriva automaticamente la configurazione del layout dalla versione desktop e i dispositivi più piccoli derivano la configurazione del layout dal telefono. Tuttavia, è possibile ignorare le configurazioni derivate automaticamente per definire una configurazione diversa per ogni tipo di dispositivo.

>[!NOTE]
>
>Se si sta creando il canale Web utilizzando [Stampa canale come master](../../forms/using/create-interactive-communication.md) per una comunicazione interattiva, i componenti disponibili per il ridimensionamento includono anche i sottomoduli e i campi generati automaticamente nel canale web utilizzando il canale Stampa. Il canale Web mantiene il layout degli elementi del canale Stampa in modalità Layout.

## Modalità Layout di accesso {#access-layout-mode}

Seleziona **Layout** dall’elenco a discesa visualizzato nella parte superiore dell’interfaccia di authoring delle comunicazioni interattive accanto al **Anteprima** opzione . Il modulo viene visualizzato in modalità Layout .

1. Accedi all&#39;istanza di authoring AEM e passa a **Adobe Experience Manager** > **Forms** > **Forms e documenti**.
1. Crea un nuovo o apri un esistente [Comunicazione interattiva](../../forms/using/create-interactive-communication.md).
1. Seleziona **Layout** dall’elenco a discesa visualizzato nella parte superiore accanto al **Anteprima** opzione . Il modulo viene visualizzato in modalità Layout .

   ![Modalità Layout per le comunicazioni interattive](assets/layout_mode_ic_new.png)

## Ridimensiona i componenti {#resize-components}

1. In modalità Layout, tocca il componente da ridimensionare. I punti blu vengono visualizzati all’inizio e alla fine della griglia reattiva.
1. Trascina i punti blu per definire la posizione del componente nella griglia reattiva.

   ![Ridimensionamento utilizzando la modalità Layout](assets/layout_mode_resize_new_updated.png)

   La barra degli strumenti visualizzata dopo aver toccato i componenti è costituita dalle seguenti opzioni:

   * **Elemento padre:** Seleziona l’elemento padre di un componente.
   * **Mobile in nuova riga:** Se sono presenti più componenti nella stessa riga, sposta il componente sulla riga successiva.

   È possibile annullare tutte le modifiche di ridimensionamento e applicare il layout predefinito al pannello contenente i componenti ridimensionati utilizzando **[!UICONTROL Ripristina layout punto di interruzione]** ( ![Ripristina punto di interruzione](assets/reverttopreviouslypublishedversion.png)). Toccare l’elemento padre del componente ridimensionato per visualizzare l’opzione .

   >[!NOTE]
   >
   >Non è possibile ridimensionare la colonna di una tabella, la barra degli strumenti, il pulsante della barra degli strumenti e i componenti dell’area di destinazione utilizzando la modalità Layout. Utilizza la modalità Stile per ridimensionare questi componenti.

### Esempio {#example}

**Obiettivo:** Inserire un componente tabella e un componente Immagine e posizionarli paralleli tra loro in una comunicazione interattiva.

1. Inserire i componenti tabella e immagine utilizzando la modalità Modifica nel canale Web di una comunicazione interattiva. Il componente Immagine viene visualizzato dopo il componente Tabella.
1. Passa alla modalità Layout e tocca il componente Tabella . I punti blu per ridimensionare il componente vengono visualizzati nelle colonne 1 e 12.
1. Trascina il punto blu nella colonna 12 alla colonna 6 della griglia reattiva.

   ![Definire il punto finale della tabella](assets/layout_mode_end_point_table_new.png)

1. Allo stesso modo, seleziona il componente Immagine e trascina il punto blu nella colonna 1 alla colonna 7 della griglia reattiva. I componenti tabella e immagine vengono visualizzati in parallelo.

   ![Tabella e immagine in parallelo in modalità Layout](assets/table_image_parallel_new.png)

   Puoi selezionare il componente Immagine e toccare il pulsante **Mobile in nuova riga** per spostare il componente Immagine sulla riga successiva, disponibile nella barra degli strumenti.

## Ridimensiona i pannelli {#resize-panels-layout-mode}

Per ridimensionare l’intero pannello invece dei singoli componenti, esegui i seguenti passaggi:

1. Tocca uno dei componenti del pannello da ridimensionare, seleziona ![Seleziona padre](assets/select_parent_icon.svg), quindi seleziona la prima opzione nell’elenco a discesa, se il pannello è l’elemento padre diretto del componente.

   I punti blu vengono visualizzati all’inizio e alla fine della griglia reattiva.

1. Trascina i punti blu per definire la posizione del pannello nella griglia reattiva.
Puoi ripetere i passaggi 1 e 2 e selezionare ![Seleziona padre](assets/float_to_new_line_icon.svg) per spostare il pannello ridimensionato alla riga successiva.

## Definire il layout a più colonne per un pannello

Esegui i seguenti passaggi per definire il numero di colonne per un pannello:

1. In **[!UICONTROL Modifica]** , tocca il pannello, seleziona ![Configura](assets/configure_icon.png), quindi seleziona **[!UICONTROL Reattivo : tutto ciò che si trova sulla pagina senza navigazione]** dall&#39;opzione **[!UICONTROL Layout del pannello]** elenco a discesa.

1. Tocca ![Salva](assets/save_icon.svg) per salvare le proprietà.

1. In **[!UICONTROL Layout]** , tocca uno dei componenti del pannello e seleziona ![Seleziona padre](assets/select_parent_icon.svg), quindi seleziona il pannello .

1. Tocca ![a più colonne](assets/multi-column.svg) e selezionare il numero di colonne dall&#39;elenco a discesa. Il numero di colonne può variare da 1 a 12. Il pannello viene diviso in un layout a più colonne.

![in modalità layout a più colonne](assets/multi-column-layout.png)

## Disattiva la modalità Layout per i moduli con layout reattivo precedente {#disable-layout-mode-for-forms-with-old-responsive-layout}

È possibile disattivare la modalità Layout per i moduli con layout reattivo precedente modificando le proprietà del modello utilizzato nel modulo.

Esegui i seguenti passaggi per disabilitare la modalità Layout :

1. Seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Modelli]** e aprire il modello utilizzato nel modulo in **[!UICONTROL Modifica]** modalità.
1. Seleziona il Contenitore documento nel riquadro a sinistra e tocca **[!UICONTROL Criterio.]**

   ![Disattiva modalità Layout](assets/policy_disable_layout_mode.png)

1. Tocca **[!UICONTROL Impostazioni layout]** e seleziona **[!UICONTROL Disattiva modalità Layout]**.
1. Tocca ![Salva modifiche](assets/save_icon.png) per salvare le proprietà del modello.
