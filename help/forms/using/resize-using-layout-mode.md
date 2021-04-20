---
title: Utilizzare la modalità Layout per ridimensionare i componenti dei moduli adattivi
description: 'Definire la posizione dei componenti utilizzando la griglia reattiva disponibile in modalità Layout '
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 0%

---


# Utilizzare la modalità Layout per ridimensionare i componenti {#use-layout-mode-to-resize-components}

L’interfaccia per la creazione di moduli adattivi consente di ridimensionare i componenti utilizzando la modalità Layout . Trascina i punti blu all’interno delle colonne per definire i punti iniziale e finale per posizionare i componenti. I punti blu vengono visualizzati dopo aver toccato il componente all’interno della griglia reattiva. La griglia reattiva è costituita da 12 colonne uguali. L’ombreggiatura del colore bianco e blu nelle colonne alternative differenzia una colonna dall’altra.

È possibile utilizzare la modalità Layout per ridimensionare i componenti per tutti i tipi di dispositivi, ad esempio desktop, tablet, telefoni e altri dispositivi più piccoli. Il tablet deriva automaticamente la configurazione del layout dalla versione desktop e i dispositivi più piccoli derivano la configurazione del layout dal telefono. Tuttavia, è possibile ignorare le configurazioni derivate automaticamente per definire una configurazione diversa per ogni tipo di dispositivo.

## Modalità Layout di accesso {#access-layout-mode}

Seleziona **Layout** dall’elenco a discesa nella parte superiore dell’interfaccia di creazione dei moduli adattivi accanto all’opzione **Anteprima**. Il modulo viene visualizzato in modalità Layout .

1. Accedi all&#39;istanza di authoring AEM e passa a **Adobe Experience Manager** > **Forms** > **Forms &amp; Documents**.
1. Crea un nuovo modulo adattivo [o apri un modulo adattivo esistente](../../forms/using/creating-adaptive-form.md).
1. Seleziona **Layout** dall&#39;elenco a discesa che viene visualizzato nella parte superiore accanto all&#39;opzione **Anteprima**. Il modulo viene visualizzato in modalità Layout .

   ![Modalità Layout](assets/layout_mode_ic_new.png)

## Ridimensiona i componenti {#resize-components}

1. In modalità Layout, tocca il componente da ridimensionare. I punti blu vengono visualizzati all’inizio e alla fine della griglia reattiva.
1. Trascina i punti blu per definire la posizione del componente nella griglia reattiva.

   ![Ridimensionamento utilizzando la modalità Layout](assets/layout_mode_resize_new_updated1.png)

   La barra degli strumenti visualizzata dopo aver toccato i componenti è costituita dalle seguenti opzioni:

   * **[!UICONTROL Elemento padre]**: Seleziona l’elemento padre di un componente.
   * **[!UICONTROL Ripristina layout]** punto di interruzione: Annulla tutte le modifiche di ridimensionamento e applica il layout predefinito al componente.
   * **[!UICONTROL Mobile in nuova riga]**: Se sono presenti più componenti nella stessa riga, sposta il componente sulla riga successiva.

   Per annullare tutte le modifiche di ridimensionamento, puoi anche utilizzare l’opzione **[!UICONTROL Ripristina layout punto di interruzione]** ( ![Ripristina punto di interruzione](assets/reverttopreviouslypublishedversion.png)) a livello di pannello.

   >[!NOTE]
   >
   >Non è possibile ridimensionare la colonna di una tabella, la barra degli strumenti, il pulsante della barra degli strumenti e i componenti dell’area di destinazione utilizzando la modalità Layout. Utilizza la modalità Stile per ridimensionare questi componenti.

### Esempio {#example}

**Obiettivo:** inserire un componente tabella e un componente immagine e posizionarli paralleli gli uni agli altri in un modulo adattivo.

1. Inserite i componenti tabella e immagine utilizzando la modalità Modifica nel modulo adattivo. Il componente Immagine viene visualizzato dopo il componente Tabella.
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

## Abilita la nuova griglia reattiva per i vecchi layout reattivi {#enableresponsivegrid}

Abilitare la nuova griglia reattiva per i moduli creati con AEM Forms 6.4 o versione precedente per ridimensionare i componenti.

>[!NOTE]
>
>Se si passa alla nuova griglia reattiva, vengono eliminate le proprietà di layout già definite per i componenti utilizzati nel modulo.

Esegui i seguenti passaggi per abilitare la nuova griglia dinamica:

1. Seleziona **Layout** dall&#39;elenco a discesa che viene visualizzato nella parte superiore accanto all&#39;opzione **Anteprima**. Viene visualizzata una conferma dell’abilitazione della modalità Layout .
1. Toccare **Sì** per attivare la modalità **Layout** del modulo.

### Incorporare un vecchio frammento in un modulo adattivo con un nuovo layout reattivo {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}

Il nuovo layout dinamico per i moduli adattivi consente di aggiungere al modulo un frammento di modulo adattivo con il vecchio layout dinamico. Tuttavia, il nuovo layout elimina le proprietà di layout già definite per i componenti utilizzati nel frammento. È possibile passare alla modalità Layout per definire le proprietà di layout dei componenti utilizzati nel frammento.

### Incorporare un frammento con un nuovo layout reattivo in un vecchio modulo adattivo {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}

Se si incorpora un frammento con il nuovo layout dinamico in un modulo adattivo con un vecchio layout dinamico, viene richiesto di abilitare la modalità Layout del modulo e di incorporarlo nuovamente.

Per abilitare la modalità Layout, seleziona **Layout** dall’elenco a discesa che viene visualizzato nella parte superiore accanto all’opzione **Anteprima** e tocca **Sì** per confermare. Seleziona la modalità **Modifica** per incorporare nuovamente il frammento.

## Disattiva la modalità Layout per i moduli con layout reattivo precedente {#disable-layout-mode-for-forms-with-old-responsive-layout}

È possibile disattivare la modalità Layout per i moduli con layout reattivo precedente modificando le proprietà del modello utilizzato nel modulo.

Esegui i seguenti passaggi per disabilitare la modalità Layout :

1. Seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Modelli]** e apri il modello utilizzato nel modulo in modalità **[!UICONTROL Modifica]**.
1. Seleziona il Contenitore documento nel riquadro a sinistra e tocca **[!UICONTROL Criterio.]**

   ![Disattiva modalità Layout](assets/policy_disable_layout_mode.png)

1. Tocca la scheda **[!UICONTROL Impostazioni layout]** e seleziona **[!UICONTROL Disattiva modalità layout]**.
1. Tocca ![Salva modifiche](assets/save_icon.png) per salvare le proprietà del modello.

