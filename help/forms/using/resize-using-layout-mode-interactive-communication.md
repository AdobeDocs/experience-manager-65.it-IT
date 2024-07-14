---
title: Utilizza la modalità Layout per ridimensionare i componenti per la comunicazione interattiva
description: Definire la posizione dei componenti utilizzando la griglia reattiva disponibile in modalità Layout
feature: Interactive Communication
exl-id: 9534fcb2-4260-4dd0-9f7e-779b10fd3a22
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---

# Utilizzare la modalità Layout per ridimensionare i componenti {#use-layout-mode-to-resize-components}

L’interfaccia di authoring del canale web di comunicazione interattiva consente di ridimensionare i componenti utilizzando la modalità Layout. Trascinate i punti blu all&#39;interno delle colonne per definire i punti iniziale e finale per posizionare i componenti. I punti blu vengono visualizzati dopo aver toccato il componente nella griglia reattiva. La griglia reattiva è costituita da 12 colonne uguali. L&#39;ombreggiatura dei colori bianco e blu nelle colonne alternative differenzia una colonna dall&#39;altra.

Puoi utilizzare la modalità Layout per ridimensionare i componenti per tutti i tipi di dispositivi, ad esempio desktop, tablet, telefono e altri dispositivi più piccoli. Il tablet deriva automaticamente la configurazione del layout dalla versione desktop e i dispositivi più piccoli derivano la configurazione del layout dal telefono. Tuttavia, puoi sovrascrivere le configurazioni derivate automaticamente per definire una configurazione diversa per ciascun tipo di dispositivo.

>[!NOTE]
>
>Se si crea il canale Web utilizzando [Canale di stampa come master](../../forms/using/create-interactive-communication.md) per una comunicazione interattiva, i componenti disponibili per il ridimensionamento includono anche i sottomoduli e i campi generati automaticamente nel canale Web utilizzando il canale di stampa. Il canale web mantiene il layout per gli elementi del canale Stampa in modalità Layout.

## Modalità Layout di accesso {#access-layout-mode}

Seleziona **Layout** dall&#39;elenco a discesa visualizzato nella parte superiore dell&#39;interfaccia di creazione delle comunicazioni interattive accanto all&#39;opzione **Anteprima**. Il modulo viene visualizzato in modalità Layout.

1. Accedi all&#39;istanza di creazione dell&#39;AEM e passa a **Adobe Experience Manager** > **Forms** > **Forms e documenti**.
1. Crea una [comunicazione interattiva](../../forms/using/create-interactive-communication.md) o apri una comunicazione esistente.
1. Seleziona **Layout** dall&#39;elenco a discesa visualizzato nella parte superiore accanto all&#39;opzione **Anteprima**. Il modulo viene visualizzato in modalità Layout.

   ![Modalità layout per le comunicazioni interattive](assets/layout_mode_ic_new.png)

## Ridimensionare i componenti {#resize-components}

1. In modalità Layout, seleziona il componente da ridimensionare. I punti blu vengono visualizzati all’inizio e alla fine della griglia reattiva.
1. Trascina i punti blu per definire la posizione del componente nella griglia reattiva.

   ![Ridimensionamento in modalità Layout](assets/layout_mode_resize_new_updated.png)

   La barra degli strumenti visualizzata dopo aver toccato i componenti è costituita dalle seguenti opzioni:

   * **Elemento padre:** Selezionare il padre di un componente.
   * **Mobile in nuova riga:** Se nella stessa riga sono presenti più componenti, spostare il componente alla riga successiva.

   Puoi annullare tutte le modifiche di ridimensionamento e applicare il layout predefinito al pannello contenente i componenti ridimensionati utilizzando l&#39;opzione **[!UICONTROL Ripristina layout punto di interruzione]** ( ![Ripristina punto di interruzione](assets/reverttopreviouslypublishedversion.png)). Seleziona l’elemento padre del componente ridimensionato per visualizzare l’opzione.

   >[!NOTE]
   >
   >Non è possibile ridimensionare i componenti colonna tabella, barra degli strumenti, pulsante barra degli strumenti e area di destinazione utilizzando la modalità Layout. Utilizza la modalità Stile per ridimensionare questi componenti.

### Esempio {#example}

**Obiettivo:** inserire un componente tabella e un componente immagine e posizionarli in modo parallelo in una comunicazione interattiva.

1. Inserisci i componenti tabella e immagine utilizzando la modalità Modifica nel canale web di una comunicazione interattiva. Il componente immagine viene visualizzato dopo il componente tabella.
1. Passa alla modalità Layout e seleziona il componente Tabella. I punti blu per ridimensionare il componente vengono visualizzati nelle colonne 1 e 12.
1. Trascina il punto blu nella colonna 12 alla colonna 6 della griglia reattiva.

   ![Definire il punto finale della tabella](assets/layout_mode_end_point_table_new.png)

1. Allo stesso modo, seleziona il componente Immagine e trascina il punto blu nella colonna 1 fino alla colonna 7 della griglia reattiva. I componenti tabella e immagine vengono visualizzati in parallelo.

   ![Tabella e immagine in parallelo in modalità Layout](assets/table_image_parallel_new.png)

   Puoi selezionare il componente Immagine e l&#39;opzione **Mobile in nuova riga** disponibile nella barra degli strumenti per spostare il componente Immagine alla riga successiva.

## Ridimensiona pannelli {#resize-panels-layout-mode}

Per ridimensionare l’intero pannello al posto dei singoli componenti, effettua le seguenti operazioni:

1. Selezionare uno dei componenti del pannello che si desidera ridimensionare, selezionare ![Seleziona elemento padre](assets/select_parent_icon.svg) e selezionare la prima opzione nell&#39;elenco a discesa, se il pannello è l&#39;elemento padre immediato del componente.

   I punti blu vengono visualizzati all’inizio e alla fine della griglia reattiva.

1. Trascina i punti blu per definire la posizione del pannello nella griglia reattiva.
È possibile ripetere i passaggi 1 e 2 e selezionare ![Seleziona elemento padre](assets/float_to_new_line_icon.svg) per spostare il pannello ridimensionato alla riga successiva.

## Definire il layout a più colonne per un pannello

Per definire il numero di colonne di un pannello, esegui i seguenti passaggi:

1. In modalità **[!UICONTROL Modifica]**, seleziona il pannello, seleziona ![Configura](assets/configure_icon.png), quindi seleziona **[!UICONTROL Reattivo - tutto nella pagina senza navigazione]** dall&#39;elenco a discesa **[!UICONTROL Layout pannello]**.

1. Seleziona ![Salva](assets/save_icon.svg) per salvare le proprietà.

1. Nella modalità **[!UICONTROL Layout]**, seleziona uno dei componenti del pannello, seleziona ![Seleziona elemento padre](assets/select_parent_icon.svg) e seleziona il pannello.

1. Selezionare ![più colonne](assets/multi-column.svg) e selezionare il numero di colonne dall&#39;elenco a discesa. Il numero di colonne può essere compreso tra 1 e 12. Il pannello viene diviso in un layout a più colonne.

![più colonne in modalità layout](assets/multi-column-layout.png)

## Disattiva la modalità Layout per i moduli con layout reattivo precedente {#disable-layout-mode-for-forms-with-old-responsive-layout}

È possibile disattivare la modalità Layout per i moduli con layout reattivo precedente modificando le proprietà del modello utilizzato nel modulo.

Per disattivare la modalità Layout, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Modelli]** e apri il modello utilizzato nel modulo in modalità **[!UICONTROL Modifica]**.
1. Selezionare il Contenitore documenti nel riquadro di sinistra e selezionare **[!UICONTROL Criterio.]**

   ![Disattiva modalità layout](assets/policy_disable_layout_mode.png)

1. Selezionare la scheda **[!UICONTROL Impostazioni layout]** e selezionare **[!UICONTROL Disattiva modalità layout]**.
1. Seleziona ![Salva modifiche](assets/save_icon.png) per salvare le proprietà del modello.
