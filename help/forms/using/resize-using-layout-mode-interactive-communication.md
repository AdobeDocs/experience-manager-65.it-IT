---
title: Utilizza la modalità Layout per ridimensionare i componenti per la comunicazione interattiva
description: Definire la posizione dei componenti utilizzando la griglia reattiva disponibile in modalità Layout
feature: Interactive Communication
exl-id: 9534fcb2-4260-4dd0-9f7e-779b10fd3a22
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---

# Utilizzare la modalità Layout per ridimensionare i componenti {#use-layout-mode-to-resize-components}

L’interfaccia di authoring del canale web di comunicazione interattiva consente di ridimensionare i componenti utilizzando la modalità Layout. Trascinate i punti blu all&#39;interno delle colonne per definire i punti iniziale e finale per posizionare i componenti. I punti blu vengono visualizzati dopo aver toccato il componente nella griglia reattiva. La griglia reattiva è costituita da 12 colonne uguali. L&#39;ombreggiatura dei colori bianco e blu nelle colonne alternative differenzia una colonna dall&#39;altra.

Puoi utilizzare la modalità Layout per ridimensionare i componenti per tutti i tipi di dispositivi, ad esempio desktop, tablet, telefono e altri dispositivi più piccoli. Il tablet deriva automaticamente la configurazione del layout dalla versione desktop e i dispositivi più piccoli derivano la configurazione del layout dal telefono. Tuttavia, puoi sovrascrivere le configurazioni derivate automaticamente per definire una configurazione diversa per ciascun tipo di dispositivo.

>[!NOTE]
>
>Se stai creando il canale web utilizzando [Stampa canale come principale](../../forms/using/create-interactive-communication.md) per una comunicazione interattiva, i componenti disponibili per il ridimensionamento includono anche i sottomoduli e i campi generati automaticamente nel canale web utilizzando il canale di stampa. Il canale web mantiene il layout per gli elementi del canale Stampa in modalità Layout.

## Modalità Layout di accesso {#access-layout-mode}

Seleziona **Layout** dall’elenco a discesa visualizzato nella parte superiore dell’interfaccia di authoring di comunicazione interattiva accanto al **Anteprima** opzione. Il modulo viene visualizzato in modalità Layout.

1. Accedi all’istanza di authoring dell’AEM e passa a **Adobe Experience Manager** > **Forms** > **Forms e documenti**.
1. Creare un [Comunicazione interattiva](../../forms/using/create-interactive-communication.md) o aprirne uno esistente.
1. Seleziona **Layout** dall&#39;elenco a discesa visualizzato nella parte superiore accanto al **Anteprima** opzione. Il modulo viene visualizzato in modalità Layout.

   ![Modalità Layout per le comunicazioni interattive](assets/layout_mode_ic_new.png)

## Ridimensionare i componenti {#resize-components}

1. In modalità Layout, seleziona il componente da ridimensionare. I punti blu vengono visualizzati all’inizio e alla fine della griglia reattiva.
1. Trascina i punti blu per definire la posizione del componente nella griglia reattiva.

   ![Ridimensionamento utilizzando la modalità Layout](assets/layout_mode_resize_new_updated.png)

   La barra degli strumenti visualizzata dopo aver toccato i componenti è costituita dalle seguenti opzioni:

   * **Elemento padre:** Seleziona l’elemento padre di un componente.
   * **Mobile in nuova riga:** Se all’interno della stessa riga sono presenti più componenti, sposta il componente sulla riga successiva.

   È possibile annullare tutte le modifiche di ridimensionamento e applicare il layout predefinito al pannello contenente i componenti ridimensionati utilizzando **[!UICONTROL Ripristina layout punto di interruzione]** ( ![Ripristina punto di interruzione](assets/reverttopreviouslypublishedversion.png)). Seleziona l’elemento padre del componente ridimensionato per visualizzare l’opzione.

   >[!NOTE]
   >
   >Non è possibile ridimensionare i componenti colonna tabella, barra degli strumenti, pulsante barra degli strumenti e area di destinazione utilizzando la modalità Layout. Utilizza la modalità Stile per ridimensionare questi componenti.

### Esempio {#example}

**Obiettivo:** Desideri inserire un componente tabella e un componente immagine e posizionarli in modo parallelo in una comunicazione interattiva.

1. Inserisci i componenti tabella e immagine utilizzando la modalità Modifica nel canale web di una comunicazione interattiva. Il componente immagine viene visualizzato dopo il componente tabella.
1. Passa alla modalità Layout e seleziona il componente Tabella. I punti blu per ridimensionare il componente vengono visualizzati nelle colonne 1 e 12.
1. Trascina il punto blu nella colonna 12 alla colonna 6 della griglia reattiva.

   ![Definire il punto finale della tabella](assets/layout_mode_end_point_table_new.png)

1. Allo stesso modo, seleziona il componente Immagine e trascina il punto blu nella colonna 1 fino alla colonna 7 della griglia reattiva. I componenti tabella e immagine vengono visualizzati in parallelo.

   ![Tabella e immagine in parallelo in modalità Layout](assets/table_image_parallel_new.png)

   Puoi selezionare il componente Immagine e quindi **Mobile in nuova riga** nella barra degli strumenti per spostare il componente Immagine alla riga successiva.

## Ridimensiona pannelli {#resize-panels-layout-mode}

Per ridimensionare l’intero pannello al posto dei singoli componenti, effettua le seguenti operazioni:

1. Seleziona uno dei componenti del pannello da ridimensionare, quindi fai clic su ![Seleziona elemento padre](assets/select_parent_icon.svg)e seleziona la prima opzione nell’elenco a discesa, se il pannello è l’elemento padre immediato del componente.

   I punti blu vengono visualizzati all’inizio e alla fine della griglia reattiva.

1. Trascina i punti blu per definire la posizione del pannello nella griglia reattiva.
È possibile ripetere i passaggi 1 e 2 e selezionare ![Seleziona elemento padre](assets/float_to_new_line_icon.svg) per spostare il pannello ridimensionato alla riga successiva.

## Definire il layout a più colonne per un pannello

Per definire il numero di colonne di un pannello, esegui i seguenti passaggi:

1. In entrata **[!UICONTROL Modifica]** , seleziona il pannello, seleziona ![Configura](assets/configure_icon.png), e seleziona **[!UICONTROL Reattivo: tutto ciò che si trova sulla pagina senza navigazione]** opzione dalla **[!UICONTROL Layout pannello]** elenco a discesa.

1. Seleziona ![Salva](assets/save_icon.svg) per salvare le proprietà.

1. In **[!UICONTROL Layout]** , seleziona uno dei componenti nel pannello, seleziona ![Seleziona elemento padre](assets/select_parent_icon.svg)e seleziona il pannello.

1. Seleziona ![a più colonne](assets/multi-column.svg) e seleziona il numero di colonne dall’elenco a discesa. Il numero di colonne può essere compreso tra 1 e 12. Il pannello viene diviso in un layout a più colonne.

![più colonne in modalità layout](assets/multi-column-layout.png)

## Disattiva la modalità Layout per i moduli con layout reattivo precedente {#disable-layout-mode-for-forms-with-old-responsive-layout}

È possibile disattivare la modalità Layout per i moduli con layout reattivo precedente modificando le proprietà del modello utilizzato nel modulo.

Per disattivare la modalità Layout, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Modelli]** e aprire il modello utilizzato nel modulo in **[!UICONTROL Modifica]** modalità.
1. Selezionare il Contenitore documenti nel riquadro a sinistra e selezionare **[!UICONTROL Politica.]**

   ![Disattiva modalità Layout](assets/policy_disable_layout_mode.png)

1. Seleziona la **[!UICONTROL Impostazioni di layout]** e seleziona **[!UICONTROL Disattiva modalità layout]**.
1. Seleziona ![Salva modifiche](assets/save_icon.png) per salvare le proprietà del modello.
