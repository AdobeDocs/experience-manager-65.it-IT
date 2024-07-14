---
title: "Tutorial: creare modelli"
description: Creazione di modelli Web e di stampa per la comunicazione interattiva
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: bef1f05e-aea2-433e-b3d5-0b7ad8163fa7
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1790'
ht-degree: 1%

---

# Tutorial: creare modelli{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Questo tutorial è un passaggio della serie [Crea la tua prima comunicazione interattiva](/help/forms/using/create-your-first-interactive-communication.md). È consigliabile seguire la serie in sequenza cronologica per comprendere, eseguire e dimostrare il caso di utilizzo completo dell’esercitazione.

Per creare una comunicazione interattiva, è necessario che sul server AEM siano disponibili modelli per la stampa e i canali Web.

I modelli per il canale di stampa vengono creati in Adobe Forms Designer e caricati sul server AEM. Questi modelli sono quindi disponibili per l’utilizzo durante la creazione di una comunicazione interattiva.

I modelli per il canale web vengono creati in AEM. Gli autori e gli amministratori dei modelli possono creare, modificare e abilitare i modelli web. Una volta creati e abilitati, questi modelli sono disponibili per l’uso durante la creazione di una comunicazione interattiva.

Questo tutorial illustra i passaggi necessari per creare modelli per i canali di stampa e web, in modo che siano disponibili per l’utilizzo durante la creazione di comunicazioni interattive. Al termine di questa esercitazione, sarai in grado di:

* Creazione di modelli XDP per il canale di stampa con Adobe Forms Designer
* Carica i modelli XDP sul server AEM Forms
* Creare e abilitare modelli per il canale web

## Crea modello per canale di stampa {#create-template-for-print-channel}

Crea e gestisci un modello per il canale di stampa della comunicazione interattiva utilizzando le seguenti attività:

* [Creare un modello XDP utilizzando Forms Designer](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [Caricare un modello XDP sul server AEM Forms](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [Creare un modello XDP per i frammenti di layout](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### Creare un modello XDP utilizzando Forms Designer {#create-xdp-template-using-forms-designer}

In base al [caso d&#39;uso](/help/forms/using/create-your-first-interactive-communication.md) e [anatomia](/help/forms/using/planning-interactive-communications.md), crea le seguenti sottomaschere nel modello XDP:

* Dettagli distinta: include un frammento di documento
* Dettagli cliente: include un frammento di documento
* Riepilogo fatture: include un frammento di documento
* Riepilogo: include un frammento di documento (sottomaschera Addebiti) e un grafico (sottomaschera Grafici)
* Chiamate dettagliate: include una tabella (frammento di layout)
* Pay Now (Paga ora): include un’immagine
* Servizi a valore aggiunto: include un’immagine

![create_print_template](assets/create_print_template.gif)

Questi sottomoduli vengono visualizzati come aree di destinazione nel modello Stampa dopo il caricamento del file XDP sul server Forms. Tutte le entità, quali frammenti di documenti, grafici, frammenti di layout e immagini, vengono aggiunte alle aree di destinazione durante la creazione della comunicazione interattiva.

Per creare un modello XDP per il canale di stampa, effettuare le seguenti operazioni:

1. Apri Forms Designer, seleziona **File** > **Nuovo** > **Utilizza un modulo vuoto,** seleziona **Avanti**, quindi seleziona **Fine** per aprire il modulo per la creazione di modelli.

   Verificare che le opzioni **Libreria oggetti** e **Oggetto** siano selezionate dal menu **Finestra**.

1. Trascinare il componente **Sottomodulo** dalla **Libreria oggetti** al modulo.
1. Selezionare la sottomaschera in modo da visualizzare le opzioni per la sottomaschera nella finestra **Oggetto** nel riquadro di destra.
1. Selezionare la scheda **Sottomodulo** e selezionare **Flusso** dall&#39;elenco a discesa **Contenuto**. Per regolare la lunghezza, trascinare il punto finale sinistro della sottomaschera.
1. Nella scheda **Associazioni**:

   1. Specifica **BillDetails** nel campo **Name**.

   1. Selezionare **Nessuna associazione dati** dall&#39;elenco a discesa **Associazione dati**.

   ![Sottomodulo Designer](assets/forms_designer_subform_new.png)

1. Analogamente, selezionare il sottomodulo principale, selezionare la scheda **Sottomodulo** e selezionare **Flusso** dall&#39;elenco a discesa **Contenuto**. Nella scheda **Associazioni**:

   1. Specificare **TelecaBill** nel campo **Name**.

   1. Selezionare **Nessuna associazione dati** dall&#39;elenco a discesa **Associazione dati**.

   ![Sottomodulo per modello di stampa](assets/root_subform_print_template_new.png)

1. Ripetere i passaggi da 2 a 5 per creare le sottomaschere seguenti:

   * Dettagli fattura
   * DettagliCliente
   * Riepilogo fatture
   * Riepilogo - Selezionare la scheda **Sottomodulo** e selezionare **Posizionato** dall&#39;elenco a discesa **Contenuto** per questo sottomodulo. Inserire le seguenti sottomaschere nella sottomaschera **Riepilogo**.

      * Spese
      * Grafici

   * Chiamate dettagliate
   * PayNow
   * ValueAddedServices

   Per risparmiare tempo, è inoltre possibile copiare e incollare sottomaschere esistenti per crearne altre.

   Per spostare la sottomaschera **Grafici** a destra della sottomaschera Spese, selezionare la sottomaschera **Grafici** dal riquadro di sinistra, selezionare la scheda **Layout** e specificare un valore per il campo **AncoraggioX**. Il valore deve essere maggiore del valore per il campo **Larghezza** della sottomaschera **Spese**. Selezionare la sottomaschera **Spese** e la scheda **Layout** per visualizzare il valore del campo **Larghezza**.

1. Trascinare l&#39;oggetto **Testo** dalla **Libreria oggetti** nel modulo e immettere **Componi XXXX per sottoscrivere** testo nella casella.
1. Fare clic con il pulsante destro del mouse sull&#39;oggetto di testo nel riquadro sinistro, selezionare **Rinomina oggetto** e immettere il nome dell&#39;oggetto di testo come **Sottoscrivi**.

   ![Modello XDP](assets/print_xdp_template_subform_new.png)

1. Selezionare **File** > **Salva con nome** per salvare il file nel file system locale:

   1. Passa alla posizione in cui è possibile salvare il file e specifica il nome come **create_first_ic_print_template**.
   1. Selezionare **.xdp** dall&#39;elenco a discesa **Salva come tipo**.

   1. Seleziona **Salva**.

### Caricare un modello XDP sul server AEM Forms {#upload-xdp-template-to-the-aem-forms-server}

Dopo aver creato un modello XDP utilizzando Forms Designer, devi caricarlo sul server AEM Forms in modo che sia disponibile per l’uso durante la creazione della comunicazione interattiva.

1. Selezionare **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Selezionare **Crea** > **Caricamento file**.

   Passa a **create_first_ic_print_template** template (XDP) e seleziona **Apri** per importare il modello XDP nel server AEM Forms.

### Creare un modello XDP per i frammenti di layout {#create-xdp-template-for-layout-fragments}

Per creare un frammento di layout per il canale di stampa della comunicazione interattiva, crea un XDP utilizzando Forms Designer e caricalo sul server AEM Forms.

1. Apri Forms Designer, seleziona **File** > **Nuovo** > **Utilizza un modulo vuoto,** seleziona **Avanti**, quindi seleziona **Fine** per aprire il modulo per la creazione di modelli.

   Verificare che le opzioni **Libreria oggetti** e **Oggetto** siano selezionate dal menu **Finestra**.

1. Trascinare il componente **Tabella** dalla **Libreria oggetti** al modulo.
1. Nella finestra di dialogo Inserisci tabella:

   1. Specificare il numero di colonne come **5**.
   1. Specificare il numero di righe del corpo come **1**.
   1. Selezionare la casella di controllo **Includi riga di intestazione nella tabella**.
   1. Scheda **OK**.

1. Selezionare **+** nel riquadro a sinistra accanto a **Tabella** 1, fare clic con il pulsante destro del mouse su **Cella1** e selezionare **Rinomina oggetto** in **Data**.

   Analogamente, rinominare rispettivamente **Cell2**, **Cell3**, **Cell4** e **Cell5** in **Time**, **Number**, **Duration** e **Charges**.

1. Fare clic sui campi di testo dell&#39;intestazione nella **Visualizzazione Designer** e rinominarli in **Tempo**, **Numero**, **Durata** e **Spese**.

   ![Frammento layout](assets/layout_fragment_print_new.png)

1. Seleziona **Riga 1** dal riquadro di sinistra e seleziona **Oggetto** > **Associazione** > **Ripeti riga per ogni elemento di dati**.

   ![Ripeti proprietà per frammento layout](assets/layout_fragment_print_repeat_new.png)

1. Trascinare il componente **Campo di testo** dalla **Libreria oggetti** alla **Visualizzazione Designer**.

   ![Campo di testo per frammento di layout](assets/layout_fragment_print_text_field_new.png)

   Analogamente, trascinare il componente **Campo di testo** nelle righe **Ora**, **Numero**, **Durata** e **Spese**.

1. Selezionare **File** > **Salva con nome** per salvare il file nel file system locale:

   1. Passa alla posizione in cui è possibile salvare il file e specifica il nome come **table_lf**.
   1. Selezionare **.xdp** dall&#39;elenco a discesa **Salva come tipo**.

   1. Seleziona **Salva**.

   Dopo aver creato un modello XDP per il frammento di layout utilizzando Forms Designer, devi [caricarlo](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server) sul server AEM Forms in modo che il modello sia disponibile per l&#39;uso durante la creazione di frammenti di layout.

## Creare un modello per il canale web {#create-template-for-web-channel}

Crea e gestisci un modello per il canale web di comunicazione interattiva utilizzando le seguenti attività:

* [Crea cartella per i modelli](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [Creare il modello](../../forms/using/create-templates-print-web.md#create-the-template)
* [Abilita il modello](../../forms/using/create-templates-print-web.md#enable-the-template)
* [Abilitazione dei pulsanti nelle comunicazioni interattive](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### Creare una cartella per i modelli {#create-folder-for-templates}

Per creare un modello di canale Web, definire una cartella in cui salvare i modelli creati. Dopo aver creato un modello all&#39;interno della cartella, abilitare il modello per consentire agli utenti dei moduli di creare un canale Web di una comunicazione interattiva basata sul modello.

Per creare una cartella per i modelli modificabili, effettuare le seguenti operazioni:

1. Seleziona **Strumenti** ![icona-martello](assets/hammer-icon.svg) > **Browser configurazioni**.
   * Per ulteriori informazioni, vedere la documentazione del [browser di configurazione](/help/sites-administering/configurations.md).
1. Nella pagina Browser configurazioni, selezionare **Crea**.
1. Nella finestra di dialogo **Crea configurazione**, specifica **Crea_Primo_IC_template** come titolo per la cartella, seleziona **Modelli modificabili** e seleziona **Crea**.

   ![Configura modelli Web](assets/create_first_ic_web_template_new.png)

   La cartella **Create_First_IC_templates** è stata creata ed elencata nella pagina **Browser configurazioni**.

### Creare il modello {#create-the-template}

In base al [caso d&#39;uso](/help/forms/using/create-your-first-interactive-communication.md) e [anatomia](/help/forms/using/planning-interactive-communications.md), crea i seguenti pannelli nel modello Web:

* Dettagli distinta: include un frammento di documento
* Dettagli cliente: include un frammento di documento
* Riepilogo fatture: include un frammento di documento
* Riepilogo addebiti: include un frammento di documento e un grafico (layout a due colonne)
* Chiamate dettagliate: include una tabella
* Pay Now: include un pulsante **Pay Now** e un&#39;immagine
* Servizi a valore aggiunto: include un&#39;immagine e un pulsante **Abbonati**.

![create_web_template](assets/create_web_template.gif)

Durante la creazione della comunicazione interattiva vengono aggiunte tutte le entità, ad esempio frammenti di documento, grafici, tabelle, immagini e pulsanti.

Per creare un modello per il canale Web nella cartella **Create_First_IC_templates**, effettuare le seguenti operazioni:

1. Passa alla cartella dei modelli appropriata selezionando la cartella **Strumenti** > **Modelli** > **Crea_Primi_IC_modelli**.
1. Seleziona **Crea**.
1. Nella configurazione guidata **Scegli un tipo di modello**, seleziona **Comunicazione interattiva - Canale Web** e seleziona **Avanti**.
1. Nella configurazione guidata **Dettagli modello**, specifica **Crea_Primo_IC_Modello_Web** come titolo del modello. Specificare una descrizione facoltativa e selezionare **Crea**.

   Messaggio di conferma della visualizzazione del **Crea_Primo_IC_Modello_Web**.

1. Seleziona **Apri** per aprire il modello nell&#39;editor modelli.
1. Selezionare **Contenuto iniziale** dall&#39;elenco a discesa accanto all&#39;opzione **Anteprima**.

   ![Editor modelli](assets/template_editor_initial_content_new.png)

1. Seleziona **Pannello principale**, quindi seleziona **+** per visualizzare l&#39;elenco dei componenti che puoi aggiungere al modello.
1. Per aggiungere un pannello sopra il **pannello principale**, seleziona **pannello** dall&#39;elenco.
1. Seleziona la scheda **Contenuto** nel riquadro a sinistra. Il nuovo pannello aggiunto al passaggio 8 viene visualizzato nel **pannello principale** nella struttura del contenuto.

   ![Struttura contenuto](assets/content_tree_root_panel_new.png)

1. Seleziona il pannello e seleziona ![configure_icon](assets/configure_icon.png) (Configura).
1. Nel riquadro Proprietà:

   1. Specifica **billdetails** nel campo Nome.
   1. Specificare **Dettagli fattura** nel campo Titolo.
   1. Selezionare **1** dall&#39;elenco a discesa **Numero di colonne**.

   1. Per salvare le proprietà, selezionare ![Salva](/help/forms/using/assets/done_icon.png).

   Il nome del pannello è stato aggiornato a **Dettagli fattura** nella struttura contenuto.

1. Ripeti i passaggi da 7 a 11 per aggiungere al modello i pannelli con le seguenti proprietà:

   | Nome | Titolo | Numero di colonne |
   |---|---|---|
   | customerdetails | Dettagli cliente | 1 |
   | billsummary | Riepilogo fatture | 1 |
   | spese di riepilogo | Riepilogo addebiti | 2 |
   | itemisedcalls | Chiamate dettagliate | 1 |
   | paynow | Paga ora | 2 |
   | area di lavoro | Servizi a valore aggiunto | 1 |

   L’immagine seguente illustra la struttura del contenuto dopo l’aggiunta di tutti i pannelli al modello:

   ![Struttura contenuto per tutti i pannelli](assets/content_tree_all_panels_new.png)

### Abilita il modello {#enable-the-template}

Dopo aver creato il modello Web, è necessario abilitarlo per utilizzarlo durante la creazione della comunicazione interattiva.

Per attivare il modello Web, eseguire le operazioni seguenti:

1. Seleziona **Strumenti** ![icona-martello](assets/hammer-icon.svg) > **Modelli**.
1. Passa al modello **Crea_Primo_IC_Modello_Web**, selezionalo e seleziona **Abilita**.
1. Seleziona di nuovo **Abilita** per confermare.

   Il modello è abilitato e il suo stato viene visualizzato come Abilitato. Puoi utilizzare questo modello durante la creazione di comunicazioni interattive per il canale web.

### Abilitazione dei pulsanti nelle comunicazioni interattive {#enabling-buttons-in-interactive-communications}

In base al caso d&#39;uso, devi includere i pulsanti **Paga ora** e **Abbonati** (componenti per moduli adattivi) nella comunicazione interattiva. Per abilitare l&#39;uso di questi pulsanti nella comunicazione interattiva, eseguire le operazioni seguenti:

1. Selezionare **Struttura** dall&#39;elenco a discesa accanto all&#39;opzione **Anteprima**.
1. Selezionare il pannello principale **Contenitore documento** utilizzando la struttura del contenuto e selezionare **Criteri** per selezionare i componenti consentiti per la comunicazione interattiva.

   ![Configura criterio](assets/structure_configure_policy_new.png)

1. Nella scheda **Componenti consentiti** della sezione **Proprietà**, seleziona **Pulsante** dai componenti **Modulo adattivo**.

   ![Componenti consentiti](assets/allowed_components_af_new.png)

1. Per salvare le proprietà, selezionare ![salva](assets/done_icon.png).
