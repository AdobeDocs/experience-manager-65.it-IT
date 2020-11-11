---
title: Utilizzare la modalità Layout per ridimensionare i componenti per i moduli adattivi
description: 'Definire la posizione dei componenti utilizzando la griglia reattiva disponibile in modalità Layout '
translation-type: tm+mt
source-git-commit: c62ad355469a95db89db44c34bb6df72d8f4bf77
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 0%

---


# Utilizzare la modalità Layout per ridimensionare i componenti {#use-layout-mode-to-resize-components}

L’interfaccia per la creazione di moduli adattivi consente di ridimensionare i componenti in modalità Layout. Trascinate i punti blu all’interno delle colonne per definire i punti iniziale e finale per posizionare i componenti. I punti blu vengono visualizzati dopo aver toccato il componente all’interno della griglia reattiva. La griglia reattiva è composta da 12 colonne uguali. L&#39;ombreggiatura del colore bianco e blu nelle colonne alternative differisce una colonna dall&#39;altra.

Potete utilizzare la modalità Layout per ridimensionare i componenti per tutti i tipi di dispositivi, ad esempio desktop, tablet, telefoni e altri dispositivi più piccoli. Il tablet deriva automaticamente la configurazione del layout dalla versione desktop e i dispositivi più piccoli derivano la configurazione del layout dal telefono. Tuttavia, potete ignorare le configurazioni derivate automaticamente per definire una configurazione diversa per ciascun tipo di dispositivo.

## Accesso alla modalità Layout {#access-layout-mode}

Selezionare **Layout** dall&#39;elenco a discesa visualizzato nella parte superiore dell&#39;interfaccia di creazione dei moduli adattivi accanto all&#39;opzione **Anteprima** . Il modulo viene visualizzato in modalità Layout.

1. Accedete all’istanza di creazione AEM e passate a **Adobe Experience Manager** > **Forms** > **Forms e documenti**.
1. Create a new or open an existing [adaptive form](../../forms/using/creating-adaptive-form.md).
1. Selezionate **Layout** dall’elenco a discesa nella parte superiore accanto all’opzione **Anteprima** . Il modulo viene visualizzato in modalità Layout.

   ![Modalità Layout](assets/layout_mode_ic_new.png)

## Ridimensiona i componenti {#resize-components}

1. In modalità Layout, toccate il componente per ridimensionarlo. I punti blu vengono visualizzati all&#39;inizio e alla fine della griglia reattiva.
1. Trascinate e rilasciate i punti blu per definire la posizione del componente nella griglia reattiva.

   ![Ridimensionamento mediante la modalità Layout](assets/layout_mode_resize_new_updated.png)

   La barra degli strumenti visualizzata dopo aver toccato i componenti è composta dalle seguenti opzioni:

   * **Elemento padre:** Selezionate l’elemento padre di un componente.
   * **Mobile in nuova riga:** Se sono presenti più componenti nella stessa riga, sposta il componente sulla riga successiva.

   Potete annullare tutte le modifiche di ridimensionamento e applicare il layout predefinito al pannello contenente i componenti ridimensionati utilizzando l’opzione **[!UICONTROL Ripristina layout]** punto di interruzione ( ![Ripristina punto di interruzione](assets/reverttopreviouslypublishedversion.png)). Toccate l’elemento padre del componente ridimensionato per visualizzare l’opzione.

   >[!NOTE]
   >
   >Non è possibile ridimensionare i componenti di colonna di tabella, barra degli strumenti, pulsante della barra degli strumenti e area di destinazione utilizzando la modalità Layout. Utilizzare la modalità Stile per ridimensionare questi componenti.

### Esempio {#example}

**Obiettivo:** Inserire un componente tabella e un componente Immagine e posizionarli parallelamente in un modulo adattivo.

1. Inserite i componenti di tabella e immagine utilizzando la modalità di modifica nel modulo adattivo. Il componente Immagine viene visualizzato dopo il componente Tabella.
1. Passate alla modalità Layout e toccate il componente Tabella. I punti blu per ridimensionare il componente vengono visualizzati nelle colonne 1 e 12.
1. Trascinate il punto blu nella colonna 12 alla colonna 6 della griglia reattiva.

   ![Definire il punto finale della tabella](assets/layout_mode_end_point_table_new.png)

1. Analogamente, selezionate il componente Immagine e trascinate il punto blu nella colonna 1 alla colonna 7 della griglia reattiva. I componenti di tabella e immagine vengono visualizzati parallelamente l’uno all’altro.

   ![Tabella e immagine in parallelo in modalità Layout](assets/table_image_parallel_new.png)

   Potete selezionare il componente Immagine e toccare l’opzione **Mobile in nuova riga** disponibile nella barra degli strumenti per spostare il componente Immagine sulla riga successiva.

## Ridimensionare i pannelli {#resize-panels-layout-mode}

Per ridimensionare l’intero pannello invece dei singoli componenti, eseguite i seguenti passaggi:

1. Toccate uno dei componenti del pannello che desiderate ridimensionare, selezionate ![Seleziona elemento padre](assets/select_parent_icon.svg), quindi selezionate la prima opzione nell’elenco a discesa, se il pannello è l’elemento padre immediato del componente.

   I punti blu vengono visualizzati all&#39;inizio e alla fine della griglia reattiva.

1. Trascinate e rilasciate i punti blu per definire la posizione del pannello nella griglia reattiva.
Potete ripetere i passaggi 1 e 2 e selezionare ![Seleziona padre](assets/float_to_new_line_icon.svg) per spostare il pannello ridimensionato sulla riga successiva.

## Definire il layout a più colonne per un pannello

Per definire il numero di colonne per un pannello, eseguite i seguenti passaggi:

1. In modalità **[!UICONTROL Modifica]** , toccate il pannello, selezionate ![Configura](assets/configure_icon.png)e selezionate **[!UICONTROL Reattivo - tutto sulla pagina senza l’opzione di navigazione]** dall’elenco a discesa Layout **** pannello.

1. Toccate ![Salva](assets/save_icon.svg) per salvare le proprietà.

1. In modalità **[!UICONTROL Layout]** , toccate uno dei componenti del pannello, selezionate ![Seleziona elemento padre](assets/select_parent_icon.svg), quindi selezionate il pannello.

1. Toccate ![più colonne](assets/multi-column.svg) e selezionate il numero di colonne dall&#39;elenco a discesa. Il numero di colonne può essere compreso tra 1 e 12. Il pannello viene diviso in un layout a più colonne.

![più colonne in modalità di layout](assets/multi-column-layout.png)

## Abilita la nuova griglia reattiva per i vecchi layout reattivi {#enableresponsivegrid}

Abilitare la nuova griglia reattiva per i moduli creati con  AEM Forms 6.4 o versione precedente per ridimensionare i componenti.

>[!NOTE]
>
>Passando alla nuova griglia reattiva, vengono eliminate le proprietà di layout già definite per i componenti utilizzati nel modulo.

Per abilitare la nuova griglia reattiva, effettuate le seguenti operazioni:

1. Selezionate **Layout** dall’elenco a discesa nella parte superiore accanto all’opzione **Anteprima** . Viene visualizzata una conferma per attivare la modalità Layout.
1. Toccate **Sì** per attivare la modalità **Layout** del modulo.

### Incorporare un vecchio frammento in un modulo adattivo con un nuovo layout reattivo {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}

Il nuovo layout reattivo per il modulo adattivo consente di aggiungere al modulo un frammento di modulo adattivo con il vecchio layout reattivo. Tuttavia, il nuovo layout elimina le proprietà di layout già definite per i componenti utilizzati nel frammento. È possibile passare alla modalità Layout per definire le proprietà di layout dei componenti utilizzati nel frammento.

### Incorporare un frammento con un nuovo layout reattivo in un vecchio modulo adattivo {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}

Se si incorpora un frammento con il nuovo layout reattivo in un modulo adattivo con un vecchio layout reattivo, viene richiesto di abilitare la modalità Layout per il modulo e di incorporarlo di nuovo.

Per attivare la modalità Layout, selezionare **Layout** dall&#39;elenco a discesa visualizzato nella parte superiore accanto all&#39;opzione **Anteprima** e toccare **Sì** per confermare. Per incorporare nuovamente il frammento, selezionare la modalità **Modifica** .

## Disattivazione della modalità Layout per i moduli con layout reattivo precedente {#disable-layout-mode-for-forms-with-old-responsive-layout}

È possibile disattivare la modalità Layout per i moduli con vecchio layout reattivo modificando le proprietà per il modello utilizzato nel modulo.

Per disattivare la modalità Layout, effettuate le seguenti operazioni:

1. Selezionare **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Modelli]** e aprire il modello utilizzato nel modulo in modalità **[!UICONTROL Modifica]** .
1. Selezionate il Contenitore documento nel riquadro a sinistra e toccate **[!UICONTROL Criterio.]**

   ![Disattiva modalità Layout](assets/policy_disable_layout_mode.png)

1. Toccate la scheda Impostazioni **[!UICONTROL di]** layout e selezionate **[!UICONTROL Disattiva modalità]** di layout.
1. Toccate ![Salva modifiche](assets/save_icon.png) per salvare le proprietà del modello.

