---
title: '"Esercitazione: Crea modelli"'
seo-title: Creare modelli di stampa e Web per comunicazioni interattive
description: Creare modelli di stampa e Web per comunicazioni interattive
seo-description: Creare modelli di stampa e Web per comunicazioni interattive
uuid: 22256a61-bcf6-4b02-9ee6-0ffb1cc20a6e
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 879ff6ca-e5f3-451d-acc2-f75142101ddd
docset: aem65
translation-type: tm+mt
source-git-commit: bd70508b361ac8b62ebc0344538a18369a075f3e
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 0%

---


# Esercitazione: Creare i modelli{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Questa esercitazione è un passaggio della serie [Create your first Interactive Communication](/help/forms/using/create-your-first-interactive-communication.md) (Creazione della prima serie di comunicazioni interattive). Si consiglia di seguire le serie in sequenza cronologica per comprendere, eseguire e dimostrare l&#39;uso completo dell&#39;esercitazione.

Per creare una comunicazione interattiva, nel server AEM per la stampa e i canali Web devono essere disponibili dei modelli.

I modelli per il canale di stampa vengono creati in Adobe Forms Designer e caricati nel server AEM. Questi modelli sono quindi disponibili per la creazione di una comunicazione interattiva.

I modelli per il canale Web vengono creati in AEM. Gli autori e gli amministratori dei modelli possono creare, modificare e abilitare i modelli Web. Una volta creati e abilitati, questi modelli sono disponibili per la creazione di una comunicazione interattiva.

Questa esercitazione illustra i passaggi necessari per creare modelli per i canali Stampa e Web in modo che siano disponibili per l&#39;utilizzo durante la creazione di comunicazioni interattive. Al termine di questa esercitazione, potrete:

* Creazione di modelli XDP per il canale di stampa tramite Adobe Forms Designer
* Caricare i modelli XDP sul server AEM Forms
* Creazione e attivazione di modelli per il canale Web

## Creare un modello per il canale di stampa {#create-template-for-print-channel}

Crea e gestisci un modello per il canale di stampa della comunicazione interattiva utilizzando le seguenti attività:

* [Creare un modello XDP utilizzando Forms Designer](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [Caricare il modello XDP sul server AEM Forms](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [Creare un modello XDP per i frammenti di layout](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### Creare un modello XDP utilizzando Forms Designer {#create-xdp-template-using-forms-designer}

In base al caso di [utilizzo](/help/forms/using/create-your-first-interactive-communication.md) e all&#39; [anatomia](/help/forms/using/planning-interactive-communications.md), creare i seguenti sottomoduli nel modello XDP:

* Dettagli fattura: Include un frammento di documento
* Dettagli cliente: Include un frammento di documento
* Riepilogo fatturazione: Include un frammento di documento
* Riepilogo: Include un frammento di documento (sottomodulo Addebiti) e un grafico (sottomodulo Grafici)
* Chiamate dettagliate: Include una tabella (frammento di layout)
* Paga ora: Include un&#39;immagine
* Servizi a valore aggiunto: Include un&#39;immagine

![create_print_template](assets/create_print_template.gif)

Questi sottomoduli vengono visualizzati come aree di destinazione nel modello di stampa dopo il caricamento del file XDP nel server Forms. Tutte le entità quali frammenti di documento, grafici, frammenti di layout e immagini vengono aggiunte alle aree di destinazione durante la creazione della comunicazione interattiva.

Per creare un modello XDP per il canale di stampa, eseguite i seguenti passaggi:

1. Aprire Forms Designer, selezionare **File** > **Nuovo** > **Usa un modulo vuoto,** toccare **Avanti**, quindi **Fine** per aprire il modulo per la creazione del modello.

   Assicurarsi che le opzioni Libreria **** oggetto e **Oggetto** siano selezionate dal menu **Finestra** .

1. Trascinare il componente **Sottomodulo** dalla Libreria **** oggetto al modulo.
1. Selezionare il sottomodulo per visualizzare le opzioni del sottomodulo nella finestra **Oggetto** , nel riquadro a destra.
1. Selezionare la scheda **Sottomodulo** e selezionare **Flusso** dall&#39;elenco a discesa **Contenuto** . Trascinare l&#39;endpoint sinistro del sottomodulo per regolare la lunghezza.
1. Nella scheda **Binding** :

   1. Specificare **BillDetails** nel campo **Nome** .

   1. Selezionare **Nessun binding** dati dall&#39;elenco a discesa Binding **** dati.

   ![Sottomodulo Designer](assets/forms_designer_subform_new.png)

1. Analogamente, selezionare il sottomodulo principale, la scheda **Sottomodulo** e selezionare **Flusso** dall&#39;elenco a discesa **Contenuto** . Nella scheda **Binding** :

   1. Specificare **TelecaBill** nel campo **Nome** .

   1. Selezionare **Nessun binding** dati dall&#39;elenco a discesa Binding **** dati.

   ![Sottomodulo per modello Stampa](assets/root_subform_print_template_new.png)

1. Ripetere i passaggi da 2 a 5 per creare i sottomoduli seguenti:

   * BillDetails
   * CustomerDetails
   * BillSummary
   * Riepilogo: selezionare la scheda **Sottomodulo** e selezionare **Posizionato** dall&#39;elenco a discesa **Contenuto** del sottomodulo. Inserire i sottomoduli seguenti nel sottomodulo **Riepilogo** .

      * Oneri
      * Grafici
   * ItemCalls
   * PayNow
   * ValueAddedServices

   Per risparmiare tempo, è inoltre possibile copiare e incollare sottomoduli esistenti per creare nuovi sottomoduli.

   Per spostare il sottomodulo **Grafici** a destra del sottomodulo Addebiti, selezionare il sottomodulo **Grafici** dal riquadro a sinistra, selezionare la scheda **Layout** e specificare un valore per il campo **AnchorX** . Il valore deve essere maggiore del valore relativo al campo **Larghezza** del sottomodulo **Addebiti** . Selezionare il sottomodulo **Addebiti** e selezionare la scheda **Layout** per visualizzare il valore del campo **Larghezza** .

1. Trascinare l&#39;oggetto **Testo** dalla Libreria **** oggetto al modulo e immettere il **Dial XXXX per sottoscrivere** il testo nella casella.
1. Fare clic con il pulsante destro del mouse sull&#39;oggetto di testo nel riquadro a sinistra, selezionare **Rinomina oggetto**, quindi immettere il nome dell&#39;oggetto di testo come **Sottoscrivi**.

   ![Modello XDP](assets/print_xdp_template_subform_new.png)

1. Selezionare **File** > **Salva con nome** per salvare il file nel file system locale:

   1. Andate alla posizione in cui salvare il file e specificate il nome come **create_first_ic_print_template**.
   1. Selezionate **.xdp** dall&#39;elenco a discesa **Salva come** .

   1. Toccate **Salva**.

### Caricare il modello XDP sul server AEM Forms {#upload-xdp-template-to-the-aem-forms-server}

Dopo aver creato un modello XDP utilizzando Forms Designer, è necessario caricarlo nel server AEM Forms in modo che sia disponibile per l&#39;uso durante la creazione della comunicazione interattiva.

1. Selezionare **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Toccate **Crea** > Caricamento **** file.

   Spostatevi e selezionate il modello **create_first_ic_print_template** (XDP), quindi toccate **Apri** per importare il modello XDP nel server AEM Forms.

### Creare un modello XDP per i frammenti di layout {#create-xdp-template-for-layout-fragments}

Per creare un frammento di layout per il canale di stampa della comunicazione interattiva, creare un file XDP utilizzando Forms Designer e caricarlo nel server AEM Forms.

1. Aprire Forms Designer, selezionare **File** > **Nuovo** > **Usa un modulo vuoto,** toccare **Avanti**, quindi **Fine** per aprire il modulo per la creazione del modello.

   Assicurarsi che le opzioni Libreria **** oggetto e **Oggetto** siano selezionate dal menu **Finestra** .

1. Trascinare il componente **Tabella** dalla Libreria **** oggetto al modulo.
1. Nella finestra di dialogo Inserisci tabella:

   1. Specificate il numero di colonne come **5**.
   1. Specificate il numero di righe corpo come **1**.
   1. Selezionare la casella di controllo **Includi riga intestazione nella tabella** .
   1. Tab **OK**.

1. Toccare **+** nel riquadro a sinistra accanto a **Tabella** 1 e fare clic con il pulsante destro del mouse su **Cella1** , quindi selezionare **Rinomina oggetto** in **data**.

   Allo stesso modo, rinominate **Cell2**, **Cell3**, **Cell4** e **Cell5** rispettivamente in **Time************** , Number, Duration, Durata, e Oneri.

1. Fare clic sui campi di testo Intestazione nella vista **di** Designer e rinominarli in **Ora**, **Numero**, **Durata** e **Addebiti**.

   ![Frammento di layout](assets/layout_fragment_print_new.png)

1. Selezionare **Riga 1** nel riquadro a sinistra, quindi **Oggetto** > **Binding** > **Ripeti riga per ogni elemento** dati.

   ![Proprietà di ripetizione per il frammento di layout](assets/layout_fragment_print_repeat_new.png)

1. Trascinare il componente Campo **di** testo dalla Libreria **** oggetto alla vista **** Designer.

   ![Campo di testo per il frammento di layout](assets/layout_fragment_print_text_field_new.png)

   Analogamente, trascinare il componente Campo **di** testo nelle righe **Ora**, **Numero**, **Durata** e **Addebito** .

1. Selezionare **File** > **Salva con nome** per salvare il file nel file system locale:

   1. Andate alla posizione in cui salvare il file e specificate il nome come **table_lf**.
   1. Selezionate **.xdp** dall&#39;elenco a discesa **Salva come** .

   1. Toccate **Salva**.
   Dopo aver creato un modello XDP per un frammento di layout utilizzando Forms Designer, è necessario [caricarlo](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server) nel server AEM Forms in modo che il modello sia disponibile per la creazione di frammenti di layout.

## Creare un modello per il canale Web {#create-template-for-web-channel}

Crea e gestisci un modello per il canale Web della comunicazione interattiva utilizzando le seguenti attività:

* [Creare una cartella per i modelli](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [Creare il modello](../../forms/using/create-templates-print-web.md#create-the-template)
* [Abilitare il modello](../../forms/using/create-templates-print-web.md#enable-the-template)
* [Abilitazione dei pulsanti nelle comunicazioni interattive](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### Creare una cartella per i modelli {#create-folder-for-templates}

Per creare un modello di canale Web, definite una cartella in cui salvare i modelli creati. Dopo aver creato un modello all&#39;interno di tale cartella, è possibile abilitare il modello per consentire agli utenti dei moduli di creare un canale Web di una comunicazione interattiva basata sul modello.

Per creare una cartella per i modelli modificabili, effettuate le seguenti operazioni:

1. Toccate **Strumenti** icona a forma di ![martello](assets/hammer-icon.svg) > **Browser** di configurazione.
1. Nella pagina del browser di configurazione, toccate **Crea**.
1. Nella finestra di dialogo **Crea configurazione** , specificate **Create_First_IC_templates** come titolo della cartella, selezionate **Modelli** modificabili e toccate **Crea**.

   ![Configurare i modelli Web](assets/create_first_ic_web_template_new.png)

   La cartella **Create_First_IC_templates** viene creata ed elencata nella pagina del browser **di** configurazione.

### Creare il modello {#create-the-template}

In base al caso di [utilizzo](/help/forms/using/create-your-first-interactive-communication.md) e all’ [anatomia](/help/forms/using/planning-interactive-communications.md), create i seguenti pannelli nel modello Web:

* Dettagli fattura: Include un frammento di documento
* Dettagli cliente: Include un frammento di documento
* Riepilogo fatturazione: Include un frammento di documento
* Riepilogo delle spese: Include un frammento di documento e un grafico (layout a due colonne)
* Chiamate dettagliate: Include una tabella
* Paga ora: Include un pulsante **Pay Now** e un&#39;immagine
* Servizi a valore aggiunto: Include un&#39;immagine e un pulsante **Iscrizione** .

![create_web_template](assets/create_web_template.gif)

Durante la creazione della comunicazione interattiva vengono aggiunte tutte le entità quali frammenti di documento, grafici, tabelle, immagini e pulsanti.

Per creare un modello per il canale Web nella cartella **Create_First_IC_templates** , effettuate le seguenti operazioni:

1. Andate alla cartella del modello appropriata selezionando **Strumenti** > **Modelli** > cartella **Create_First_IC_templates** .
1. Toccate **Crea**.
1. Nella procedura guidata di configurazione **Scegli un tipo** di modello, seleziona Comunicazione **interattiva - Canale** Web e tocca **Avanti**.
1. Nella procedura guidata di configurazione Dettagli **** modello, specificate **Create_First_IC_Web_Template** come titolo del modello. Specificate una descrizione facoltativa e toccate **Crea**.

   Viene visualizzato un messaggio di conferma della visualizzazione di **Create_First_IC_Web_Template** .

1. Toccate **Apri** per aprire il modello nell’editor modelli.
1. Selezionate Contenuto **** iniziale dall’elenco a discesa accanto all’opzione **Anteprima** .

   ![Editor modelli](assets/template_editor_initial_content_new.png)

1. Toccate Pannello **** principale e quindi toccate **+** per visualizzare l’elenco dei componenti che potete aggiungere al modello.
1. Selezionate **Pannello** dall’elenco per aggiungere un pannello sopra il pannello **** principale.
1. Selezionate la scheda **Contenuto** nel riquadro a sinistra. Il nuovo pannello aggiunto al punto 8 viene visualizzato sotto il pannello **** Principale nella struttura del contenuto.

   ![Struttura contenuto](assets/content_tree_root_panel_new.png)

1. Selezionate il pannello e toccate ![configure_icon](assets/configure_icon.png) (Configura).
1. Nel riquadro Proprietà:

   1. Specificate **i dettagli** fatturati nel campo Nome.
   1. Specificate Dettagli **** fatturazione nel campo Titolo.
   1. Selezionare **1** dall&#39;elenco a discesa **Numero di colonne** .

   1. Toccate ![](/help/forms/using/assets/done_icon.png) per salvare le proprietà.

   Il nome del pannello viene aggiornato in Dettagli **** fatturazione nella struttura del contenuto.

1. Ripetete i passaggi da 7 a 11 per aggiungere al modello i pannelli con le seguenti proprietà:

   | Nome | Titolo | Numero di colonne |
   |---|---|---|
   | dettagli cliente | Dettagli cliente | 1 |
   | billsummary | Riepilogo fatturazione | 1 |
   | riepiloghi | Riepilogo delle spese | 2 |
   | itemisedCalls | Chiamate dettagliate | 1 |
   | paynow | Paga ora | 2 |
   | vas | Servizi a valore aggiunto | 1 |

   L&#39;immagine seguente rappresenta la struttura del contenuto dopo l&#39;aggiunta di tutti i pannelli al modello:

   ![Struttura del contenuto per tutti i pannelli](assets/content_tree_all_panels_new.png)

### Abilitare il modello {#enable-the-template}

Dopo aver creato il modello Web, è necessario attivarlo per utilizzare il modello durante la creazione della comunicazione interattiva.

Per abilitare il modello Web, eseguite i seguenti passaggi:

1. Toccare **Strumenti** icona a forma di ![martello](assets/hammer-icon.svg) > **Modelli**.
1. Individuate il modello **Create_First_IC_Web_Template** , selezionatelo e toccate **Abilita**.
1. Scheda **Abilita** di nuovo per confermare.

   Il modello è abilitato e il suo stato viene visualizzato come Abilitato. Potete utilizzare questo modello durante la creazione di comunicazioni interattive per il canale Web.

### Abilitazione dei pulsanti nelle comunicazioni interattive {#enabling-buttons-in-interactive-communications}

In base al caso di utilizzo, nella comunicazione interattiva è necessario includere i pulsanti **Paga ora** e **Iscrizione** (componenti per moduli adattivi). Per abilitare l&#39;utilizzo di questi pulsanti nella comunicazione interattiva, eseguire i seguenti passaggi:

1. Selezionate **Struttura** dall’elenco a discesa accanto all’opzione **Anteprima** .
1. Selezionate il pannello principale Contenitore **** documento utilizzando la struttura del contenuto e toccate **Criterio** per selezionare i componenti utilizzabili nella comunicazione interattiva.

   ![Configurare il criterio](assets/structure_configure_policy_new.png)

1. Nella scheda Componenti **** consentiti della sezione **Proprietà** , selezionare **Pulsante** dai componenti Modulo **** adattivo.

   ![Componenti consentiti](assets/allowed_components_af_new.png)

1. Toccate ![done_icon](assets/done_icon.png) per salvare le proprietà.