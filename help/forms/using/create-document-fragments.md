---
title: "Tutorial: creare frammenti di documento"
seo-title: Create document fragments for Interactive Communication
description: Creare frammenti di documenti per la comunicazione interattiva
seo-description: Create document fragments for Interactive Communication
uuid: 677d717e-e92e-434e-8266-6fbbf94f3867
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8ae97a21-83af-4615-9be3-61e2f8065081
docset: aem65
feature: Interactive Communication
exl-id: 81429735-cd52-4621-8dc2-10dd89df3052
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 2%

---

# Tutorial: creare frammenti di documento{#tutorial-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Questo tutorial è un passaggio del [Creare la prima comunicazione interattiva](/help/forms/using/create-your-first-interactive-communication.md) serie. Si consiglia di seguire la serie in sequenza cronologica per comprendere, eseguire e dimostrare il caso di utilizzo completo dell’esercitazione.

I frammenti di documento sono componenti riutilizzabili di una corrispondenza utilizzati per comporre una comunicazione interattiva. I frammenti di documento sono dei seguenti tipi:

* Testo: una risorsa di testo è un contenuto costituito da uno o più paragrafi di testo. Un paragrafo può essere statico o dinamico.
* Elenco: l’elenco è un gruppo di frammenti di documento, inclusi testo, elenchi, condizioni e immagini.
* Condizione: le condizioni ti consentono di definire quale contenuto viene incluso nella comunicazione interattiva in base ai dati ricevuti dal modello di dati del modulo.

Questo tutorial illustra i passaggi necessari per creare più frammenti di documenti di testo in base all’anatomia fornita in [Pianificare la comunicazione interattiva](/help/forms/using/planning-interactive-communications.md) sezione. Al termine di questa esercitazione, sarai in grado di:

* Creare frammenti di documenti
* Creare le variabili
* Creare e applicare regole

![text_document_fragments](assets/text_document_fragments.gif)

Di seguito è riportato l’elenco dei frammenti di documento creati in questa esercitazione:

* [Dettagli fattura](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [Dettagli cliente](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [Riepilogo fatture](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [Riepilogo delle spese](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

Ogni frammento di documento include campi con testo statico, dati ricevuti dal modello di dati del modulo e dati immessi tramite l’interfaccia utente dell’agente. Tutti questi campi sono stati rappresentati nel [Pianificare la comunicazione interattiva](/help/forms/using/planning-interactive-communications.md) sezione.

Durante la creazione di frammenti di documento in questa esercitazione, vengono create variabili per i campi che ricevono dati tramite l’interfaccia utente dell’agente.

Utilizzare **FDM_Create_First_IC**, come descritto nella [Crea modello dati modulo](../../forms/using/create-form-data-model0.md) come modello dati modulo per creare frammenti di documento in questa esercitazione.

## Passaggio 1: creare un frammento di documento di testo Dettagli fattura {#step-create-bill-details-text-document-fragment}

Il frammento di documento Dettagli distinta include i campi seguenti:

| Campo | Sorgente dati |
|---|---|
| N. fattura | Interfaccia utente agente |
| Periodo di fatturazione | Interfaccia utente agente |
| Data di fatturazione | Interfaccia utente agente |
| Il piano | Modello dati modulo |

Esegui la procedura seguente per creare variabili per i campi con l’interfaccia utente di Agent come origine dati, creare testo statico e utilizzare gli elementi del modello dati del modulo nel frammento di documento:

1. Seleziona **[!UICONTROL Forms]** > **[!UICONTROL Frammenti di documenti]**.

1. Seleziona **Crea** > **Testo**.
1. Specifica le seguenti informazioni:

   1. Invio **bill_details_first_ic** come nome nella sezione **Titolo** campo. Il titolo viene popolato automaticamente in **Nome** campo.

   1. Seleziona **Modello dati modulo** dal **Modello dati** sezione.

   1. Seleziona **FDM_Create_First_IC** come modello di dati del modulo e tocca **Seleziona**.

   1. Tocca **Successivo**.

1. Seleziona la **Variabili** nel riquadro a sinistra e tocca **Crea**.
1. In **Crea variabile** sezione:

   1. Invio **Invoicenum** come nome della variabile.
   1. Seleziona **Stringa** come tipo.
   1. Tocca **Crea**.

   ![Crea variabile di tipo stringa](assets/variable_create_string_new.png)

   Ripeti i passaggi 4 e 5 per creare le seguenti variabili:

   * Billperiod: tipo di stringa
   * Data fatturazione: tipo di data

   ![Dettagli fattura](assets/variable_bill_details_new.png)

1. Crea testo statico per i campi seguenti utilizzando il riquadro di destra:

   * N. fattura
   * Periodo di fatturazione
   * Data di fatturazione
   * Il piano

   ![Testo statico](assets/variable_bill_details_static_text_new.png)

1. Posizionare il cursore accanto al **N. fattura** e fare doppio clic sul **Numero fattura** variabile dalla **Variabili** nel riquadro a sinistra.
1. Posizionare il cursore accanto al **Periodo di fatturazione** e fare doppio clic sul **Periodo di fatturazione** variabile.
1. Posizionare il cursore accanto al **Data di fatturazione** e fare doppio clic sul **Data di fatturazione** variabile.
1. Seleziona la **Oggetti modello dati** nel riquadro a sinistra.
1. Posizionare il cursore accanto al **Il piano** e fare doppio clic sul **cliente** > **customerplan** proprietà.

   ![bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. Clic **Salva** per creare il frammento di documento di testo Dettagli distinta.

## Passaggio 2: creare un frammento del documento di testo Dettagli cliente {#step-create-customer-details-text-document-fragment}

Il frammento di documento Dettagli cliente include i campi seguenti:

| Campo | Sorgente dati |
|---|---|
| Nome cliente | Modello dati modulo |
| Indirizzo | Modello dati modulo |
| Luogo della prestazione | Interfaccia utente agente |
| Codice stato | Interfaccia utente agente |
| Numero cellulare | Modello dati modulo |
| Numero di contatto alternativo | Modello dati modulo |
| Numero di relazione | Modello dati modulo |
| Numero di connessioni | Interfaccia utente agente |

Esegui la procedura seguente per creare variabili per i campi con l’interfaccia utente di Agent come origine dati, creare testo statico e utilizzare gli elementi del modello dati del modulo nel frammento di documento:

1. Seleziona **[!UICONTROL Forms]** > **[!UICONTROL Frammenti di documenti]**.
1. Seleziona **Crea** > **Testo**.
1. Specifica le seguenti informazioni:

   1. Invio **customer_details_first_ic** come nome nella sezione **Titolo** campo. Il titolo viene popolato automaticamente in **Nome** campo.

   1. Seleziona **Modello dati modulo** dal **Modello dati** sezione.

   1. Seleziona **FDM_Create_First_IC** come modello di dati del modulo e tocca **Seleziona**.

   1. Tocca **Successivo**.

1. Seleziona la **Variabili** nel riquadro a sinistra e tocca **Crea**.
1. In **Crea variabile** sezione:

   1. Invio **Placesupply** come nome della variabile.
   1. Seleziona **Stringa** come tipo.
   1. Tocca **Crea**.

   Ripeti i passaggi 4 e 5 per creare le seguenti variabili:

   * Codice stato: tipo di numero
   * Numberconnections: tipo di numero


1. Seleziona la **Oggetti modello dati** , posizionare il cursore nel riquadro di destra e fare doppio clic sulla **cliente** > **nome** proprietà.
1. Premere Invio per spostare il cursore sulla riga successiva e fare doppio clic sulla **cliente** > **indirizzo** proprietà.
1. Crea testo statico per i campi seguenti utilizzando il riquadro di destra:

   * Numero cellulare
   * Numero di contatto alternativo
   * Luogo della prestazione
   * Numero di relazione
   * Codice stato
   * Numero di connessioni

   ![Testo statico dettagli cliente](assets/customer_details_static_text_new.png)

1. Posizionare il cursore accanto al **Numero cellulare** e fare doppio clic sul **cliente** > **mobilenum** proprietà.
1. Posizionare il cursore accanto al **Numero di contatto alternativo** e fai doppio clic su** cliente** > **alternate obilenumber** proprietà.
1. Posizionare il cursore accanto al **Numero di relazione** e fare doppio clic sul **cliente** > **numero relazione** proprietà.
1. Seleziona la **Variabili** , posizionare il cursore accanto al **Luogo della prestazione** e fare doppio clic sul **Placesupply** variabile.
1. Posizionare il cursore accanto al **Codice stato** e fare doppio clic sul **Codice di stato** variabile.
1. Posizionare il cursore accanto al **Numero di connessioni** e fare doppio clic sul **Numberconnections** variabile.

   ![Dettagli cliente](assets/customer_details_df2_new.png)

1. Clic **Salva** per creare il frammento del documento di testo Dettagli cliente.

## Passaggio 3: creare un frammento di documento di riepilogo delle fatture {#step-create-bill-summary-text-document-fragment}

Il frammento di documento Riepilogo fatture include i campi riportati di seguito.

| Campo | Sorgente dati |
|---|---|
| Saldo precedente | Interfaccia utente agente |
| Pagamenti | Interfaccia utente agente |
| Adeguamenti | Interfaccia utente agente |
| Addebiti periodo di fatturazione corrente | Modello dati modulo |
| Importo dovuto | Interfaccia utente agente |
| Data di scadenza | Interfaccia utente agente |

Esegui la procedura seguente per creare variabili per i campi con l’interfaccia utente di Agent come origine dati, creare testo statico e utilizzare gli elementi del modello dati del modulo nel frammento di documento:

1. Seleziona **[!UICONTROL Forms]** > **[!UICONTROL Frammenti di documenti]**.
1. Seleziona **Crea** > **Testo**.
1. Specifica le seguenti informazioni:

   1. Invio **bill_summary_first_ic** come nome nella sezione **Titolo** campo. Il titolo viene popolato automaticamente in **Nome** campo.

   1. Seleziona **Modello dati modulo** dal **Modello dati** sezione.

   1. Seleziona **FDM_Create_First_IC** come modello di dati del modulo e tocca **Seleziona**.

   1. Tocca **Successivo**.

1. Seleziona la **Variabili** nel riquadro a sinistra e tocca **Crea**.
1. In **Crea variabile** sezione:

   1. Invio **Saldo precedente** come nome della variabile.
   1. Seleziona **Numero** come tipo.
   1. Tocca **Crea**.

   Ripeti i passaggi 4 e 5 per creare le seguenti variabili:

   * Pagamenti: tipo di numero
   * Adeguamenti: tipo di numero
   * Importo: tipo di numero
   * Data scadenza: tipo di data


1. Crea testo statico per i campi seguenti utilizzando il riquadro di destra:

   * Saldo precedente
   * Pagamenti
   * Adeguamenti
   * Addebiti periodo di fatturazione corrente
   * Importo dovuto
   * Data di scadenza
   * Le spese di pagamento in ritardo dopo la data di scadenza sono pari a $ 20

   ![Testo statico Riepilogo fatture](assets/bill_summary_static_new.png)

1. Posizionare il cursore accanto al **Saldo precedente** e fare doppio clic sul **Saldo precedente** variabile.
1. Posizionare il cursore accanto al **Pagamenti** e fare doppio clic sul **Pagamenti** variabile.
1. Posizionare il cursore accanto al **Adeguamenti** e fare doppio clic sul **Adeguamenti** variabile.
1. Posizionare il cursore accanto al **Importo dovuto** e fare doppio clic sul **Importo dovuto** variabile.
1. Posizionare il cursore accanto al **Data di scadenza** e fare doppio clic sul **Duedate** variabile.
1. Seleziona la **Oggetti modello dati** , posizionare il cursore accanto al **Addebiti periodo di fatturazione corrente** nel riquadro di destra e fare doppio clic sul **effetti** > **spese d&#39;uso** proprietà.

   ![Riepilogo fatture](assets/bill_summary_static_variables_new.png)

1. Clic **Salva** per creare il frammento del documento di testo Dettagli cliente.

## Passaggio 4: creare un frammento di documento di testo per il riepilogo delle spese {#step-create-summary-of-charges-text-document-fragment}

Il frammento di documento Riepilogo spese include i campi seguenti:

| Campo | Sorgente dati |
|---|---|
| Spese di chiamata | Modello dati modulo |
| Spese di conferenza telefonica | Modello dati modulo |
| Spese SMS | Modello dati modulo |
| Tariffe Internet mobile | Modello dati modulo |
| Tariffe nazionali di roaming | Modello dati modulo |
| Tariffe di roaming internazionale | Modello dati modulo |
| Spese per servizi a valore aggiunto | Modello dati modulo |
| Oneri totali | Modello dati modulo |
| TOTALE DA PAGARE | Modello dati modulo |

Per creare testo statico e utilizzare gli elementi del modello dati modulo nel frammento di documento, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Forms]** > **[!UICONTROL Frammenti di documenti]**.
1. Seleziona **Crea** > **Testo**.
1. Specifica le seguenti informazioni:

   1. Invio **summary_charge_first_ic** come nome nella sezione **Titolo** campo. Il titolo viene compilato automaticamente nel campo Nome.

   1. Seleziona **Modello dati modulo** dal **Modello dati** sezione.

   1. Seleziona **FDM_Create_First_IC** come modello di dati del modulo e tocca **Seleziona**.

   1. Tocca **Successivo**.

1. Crea testo statico per i campi seguenti utilizzando il riquadro di destra:

   * Spese di chiamata
   * Spese di conferenza telefonica
   * Spese SMS
   * Tariffe Internet mobile
   * Tariffe nazionali di roaming
   * Tariffe di roaming internazionale
   * Spese per servizi a valore aggiunto
   * Oneri totali
   * TOTALE DA PAGARE

   ![Oneri di riepilogo](assets/summary_charges_static_new.png)

1. Seleziona la **Oggetti modello dati** scheda.
1. Posizionare il cursore accanto al **Spese di chiamata** e fare doppio clic sul **effetti** > **callcharge** proprietà.
1. Posizionare il cursore accanto al **Spese di conferenza telefonica** e fare doppio clic sul **effetti** > **confcallcharge** proprietà.
1. Posizionare il cursore accanto al **Spese SMS** e fare doppio clic sul **effetti** > **schemi** proprietà.
1. Posizionare il cursore accanto al **Tariffe Internet mobile** e fare doppio clic sul **effetti** > **tariffe Internet** proprietà.
1. Posizionare il cursore accanto al **Tariffe nazionali di roaming** e fare doppio clic sul **effetti** > **roamingnational** proprietà.
1. Posizionare il cursore accanto al **Tariffe di roaming internazionale** e fare doppio clic sul **effetti** > **roaming** proprietà.
1. Posizionare il cursore accanto al **Spese per servizi a valore aggiunto** e fare doppio clic sul **effetti** > **area di lavoro** proprietà.
1. Posizionare il cursore accanto al **Oneri totali** e fare doppio clic sul **effetti** > **spese d&#39;uso** proprietà.
1. Posizionare il cursore accanto al **TOTALE DA PAGARE** e fare doppio clic sul **effetti** > **spese d&#39;uso** proprietà.

   ![Riepilogo addebiti](assets/summary_charges_static_fdm_new.png)

1. Seleziona il testo nella **Spese per servizi a valore aggiunto** riga e tocca **Crea regola** per creare una condizione in base alla quale visualizzare la riga nella comunicazione interattiva:
1. Il giorno **Crea regola** finestra popup:

   1. Seleziona **Modelli di dati e variabili** e poi **effetti** > **callcharge**.

   1. Seleziona **è minore di** come operatore.
   1. Seleziona **Numero** e inserisci il valore come **60**.

   In base a questa condizione, la riga Spese servizi a valore aggiunto viene visualizzata solo se il valore del campo Spese di chiamata è inferiore a 60.

   ![create_rules_caption](assets/create_rules_caption.gif)

1. Clic **Salva** per creare il frammento di documento di testo Riepilogo spese.
