---
title: '"Esercitazione: Crea frammenti di documento"'
seo-title: Creazione di frammenti di documento per la comunicazione interattiva
description: Creazione di frammenti di documento per la comunicazione interattiva
seo-description: Creazione di frammenti di documento per la comunicazione interattiva
uuid: 677d717e-e92e-434e-8266-6fbbf94f3867
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8ae97a21-83af-4615-9be3-61e2f8065081
docset: aem65
translation-type: tm+mt
source-git-commit: e545fc5e2ea139bd8ebb7f84138ba68e03d71d19
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 2%

---


# Esercitazione: Creare frammenti di documento{#tutorial-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Questa esercitazione è un passaggio della serie [Crea la tua prima comunicazione interattiva](/help/forms/using/create-your-first-interactive-communication.md). Si consiglia di seguire le serie in sequenza cronologica per comprendere, eseguire e dimostrare l&#39;uso completo dell&#39;esercitazione.

I frammenti di documento sono componenti riutilizzabili di una corrispondenza utilizzata per comporre una comunicazione interattiva. I frammenti di documento sono dei tipi seguenti:

* Testo: una risorsa di testo è un contenuto costituito da uno o più paragrafi di testo. Un paragrafo può essere statico o dinamico.
* Elenco - Elenco è un gruppo di frammenti di documento, inclusi testo, elenchi, condizioni e immagini.
* Condizione: le condizioni consentono di definire il contenuto da includere nella comunicazione interattiva in base ai dati ricevuti dal modello dati del modulo.

Questa esercitazione illustra i passaggi necessari per creare più frammenti di documento di testo in base all&#39;anatomia fornita nella sezione [Pianificare la comunicazione interattiva](/help/forms/using/planning-interactive-communications.md). Al termine di questa esercitazione, potrete:

* Creazione di frammenti di documento
* Creare variabili
* Creazione e applicazione di regole

![text_document_fragments](assets/text_document_fragments.gif)

Di seguito è riportato l&#39;elenco dei frammenti di documento creati con questa esercitazione:

* [Dettagli fattura](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [Dettagli cliente](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [Riepilogo fatturazione](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [Riepilogo delle spese](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

Ciascun frammento di documento include campi con testo statico, dati ricevuti dal modello dati del modulo e dati immessi tramite l&#39;interfaccia utente dell&#39;agente. Tutti questi campi sono stati rappresentati nella sezione [Pianificare la comunicazione interattiva](/help/forms/using/planning-interactive-communications.md).

Durante la creazione di frammenti di documento in questa esercitazione, vengono create variabili per i campi che ricevono dati tramite l&#39;interfaccia utente dell&#39;agente.

In questa esercitazione, utilizzare **FDM_Create_First_IC**, come descritto nella sezione [Crea modello dati modulo](../../forms/using/create-form-data-model0.md), come modello dati modulo per creare frammenti di documento.

## Passaggio 1: Crea frammento di testo del documento Dettagli fatturazione {#step-create-bill-details-text-document-fragment}

Il frammento di documento Dettagli fatturazione include i campi seguenti:

| Campo | Sorgente dati |
|---|---|
| Numero fattura | Interfaccia utente agente |
| Periodo fatturazione | Interfaccia utente agente |
| Data fatturazione | Interfaccia utente agente |
| Il tuo piano | Modello dati modulo |

Per creare variabili per i campi con l’interfaccia utente agente come origine dati, creare testo statico e utilizzare gli elementi del modello dati del modulo nel frammento di documento, procedere come segue:

1. Selezionare **[!UICONTROL Forms]** > **[!UICONTROL Frammenti documento]**.

1. Selezionare **Crea** > **Testo**.
1. Specificate le seguenti informazioni:

   1. Immettere **bill_details_first_ic** come nome nel campo **Title**. Il titolo viene compilato automaticamente nel campo **Name**.

   1. Selezionare **Form Data Model** dalla sezione **Data Model**.

   1. Selezionare **FDM_Create_First_IC** come modello dati modulo e toccare **Seleziona**.

   1. Toccare **Next**.

1. Selezionare la scheda **Variabili** nel riquadro a sinistra e toccare **Crea**.
1. Nella sezione **Crea variabile**:

   1. Immettere **Numero di fattura** come nome della variabile.
   1. Selezionare **String** come tipo.
   1. Toccate **Crea**.

   ![Crea variabile di tipo String](assets/variable_create_string_new.png)

   Ripetere i passaggi 4 e 5 per creare le seguenti variabili:

   * Periodo di fatturazione: Tipo stringa
   * Data fatturazione: Tipo data

   ![Dettagli fattura](assets/variable_bill_details_new.png)

1. Utilizzando il riquadro a destra, potete creare testo statico per i seguenti campi:

   * Numero fattura
   * Periodo fatturazione
   * Data fatturazione
   * Il tuo piano

   ![Testo statico](assets/variable_bill_details_static_text_new.png)

1. Posizionare il cursore accanto al campo **Nr. fattura** e fare doppio clic sulla variabile **InvoiceNumber** dalla scheda **Variabili** nel riquadro a sinistra.
1. Posizionare il cursore accanto al campo **Periodo fatturazione** e fare doppio clic sulla variabile **Billpunto**.
1. Posizionare il cursore accanto al campo **Data fatturazione** e fare doppio clic sulla variabile **Data fatturazione**.
1. Selezionare la scheda **Oggetti modello dati** nel riquadro a sinistra.
1. Posizionare il cursore accanto al campo **Piano** e fare doppio clic sulla proprietà **customer** > **customerplan**.

   ![bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. Fare clic su **Salva** per creare il frammento di testo Dettagli fatturazione.

## Passaggio 2: Crea frammento di testo del documento Dettagli cliente {#step-create-customer-details-text-document-fragment}

Il frammento di documento Dettagli cliente include i campi seguenti:

| Campo | Sorgente dati |
|---|---|
| Nome cliente | Modello dati modulo |
| Indirizzo | Modello dati modulo |
| Luogo di fornitura | Interfaccia utente agente |
| Codice di stato | Interfaccia utente agente |
| Numero cellulare | Modello dati modulo |
| Numero di contatto alternativo | Modello dati modulo |
| Numero relazione | Modello dati modulo |
| Numero di connessioni | Interfaccia utente agente |

Per creare variabili per i campi con l’interfaccia utente agente come origine dati, creare testo statico e utilizzare gli elementi del modello dati del modulo nel frammento di documento, procedere come segue:

1. Selezionare **[!UICONTROL Forms]** > **[!UICONTROL Frammenti documento]**.
1. Selezionare **Crea** > **Testo**.
1. Specificate le seguenti informazioni:

   1. Immettere **customer_details_first_ic** come nome nel campo **Title**. Il titolo viene compilato automaticamente nel campo **Name**.

   1. Selezionare **Form Data Model** dalla sezione **Data Model**.

   1. Selezionare **FDM_Create_First_IC** come modello dati modulo e toccare **Seleziona**.

   1. Toccare **Next**.

1. Selezionare la scheda **Variabili** nel riquadro a sinistra e toccare **Crea**.
1. Nella sezione **Crea variabile**:

   1. Immettere **Placesupply** come nome della variabile.
   1. Selezionare **String** come tipo.
   1. Toccate **Crea**.

   Ripetere i passaggi 4 e 5 per creare le seguenti variabili:

   * Codice di stato: Tipo di numero
   * Numberconnection: Tipo di numero


1. Selezionare la scheda **Oggetti modello dati**, posizionare il cursore nel riquadro a destra e fare doppio clic sulla proprietà **customer** > **name**.
1. Premere Invio per spostare il cursore sulla riga successiva e fare doppio clic sulla proprietà **customer** > **address**.
1. Utilizzando il riquadro a destra, potete creare testo statico per i seguenti campi:

   * Numero cellulare
   * Numero di contatto alternativo
   * Luogo di fornitura
   * Numero relazione
   * Codice di stato
   * Numero di connessioni

   ![Testo statico dei dettagli del cliente](assets/customer_details_static_text_new.png)

1. Posizionare il cursore accanto al campo **Numero mobile** e fare doppio clic sulla proprietà **customer** > **mobilenum**.
1. Posizionare il cursore accanto al campo **Numero di contatto alternativo** e fare doppio clic sulla proprietà** customer** > **numero di telefono alternativo**.
1. Posizionare il cursore accanto al campo **Numero relazione**, quindi fare doppio clic sulla proprietà **customer** > **relation number**.
1. Selezionare la scheda **Variabili**, posizionare il cursore accanto al campo **Luogo di fornitura** e fare doppio clic sulla variabile **Placesupply**.
1. Posizionare il cursore accanto al campo **Codice di stato** e fare doppio clic sulla variabile **Codice di stato**.
1. Posizionare il cursore accanto al campo **Numero di connessioni** e fare doppio clic sulla variabile **NumberConnections**.

   ![Dettagli cliente](assets/customer_details_df2_new.png)

1. Fare clic su **Salva** per creare il frammento del documento di testo Dettagli cliente.

## Passaggio 3: Crea frammento di testo di riepilogo distinta {#step-create-bill-summary-text-document-fragment}

Il frammento di documento Riepilogo fatturazione include i campi seguenti:

| Campo | Sorgente dati |
|---|---|
| Saldo precedente | Interfaccia utente agente |
| Pagamenti | Interfaccia utente agente |
| Regolazioni | Interfaccia utente agente |
| Addebito periodo corrente | Modello dati modulo |
| Importo dovuto | Interfaccia utente agente |
| Data di scadenza | Interfaccia utente agente |

Per creare variabili per i campi con l’interfaccia utente agente come origine dati, creare testo statico e utilizzare gli elementi del modello dati del modulo nel frammento di documento, procedere come segue:

1. Selezionare **[!UICONTROL Forms]** > **[!UICONTROL Frammenti documento]**.
1. Selezionare **Crea** > **Testo**.
1. Specificate le seguenti informazioni:

   1. Immettere **bill_summary_first_ic** come nome nel campo **Title**. Il titolo viene compilato automaticamente nel campo **Name**.

   1. Selezionare **Form Data Model** dalla sezione **Data Model**.

   1. Selezionare **FDM_Create_First_IC** come modello dati modulo e toccare **Seleziona**.

   1. Toccare **Next**.

1. Selezionare la scheda **Variabili** nel riquadro a sinistra e toccare **Crea**.
1. Nella sezione **Crea variabile**:

   1. Immettere **Precedente bilancio** come nome della variabile.
   1. Selezionare **Number** come tipo.
   1. Toccate **Crea**.

   Ripetere i passaggi 4 e 5 per creare le seguenti variabili:

   * Pagamenti: Tipo di numero
   * Regolazioni: Tipo di numero
   * Amontdue: Tipo di numero
   * Duedate: Tipo data


1. Utilizzando il riquadro a destra, potete creare testo statico per i seguenti campi:

   * Saldo precedente
   * Pagamenti
   * Regolazioni
   * Addebito periodo corrente
   * Importo dovuto
   * Data di scadenza
   * Le spese di pagamento tardivo dopo la data di scadenza sono $ 20

   ![Testo statico Riepilogo distinte](assets/bill_summary_static_new.png)

1. Posizionare il cursore accanto al campo **Saldo precedente** e fare doppio clic sulla variabile **Bilanciamento precedente**.
1. Posizionare il cursore accanto al campo **Pagamenti** e fare doppio clic sulla variabile **Pagamenti**.
1. Posizionare il cursore accanto al campo **Regolazioni** e fare doppio clic sulla variabile **Regolazioni**.
1. Posizionare il cursore accanto al campo **Importo dovuto** e fare doppio clic sulla variabile **Amontdue**.
1. Posizionare il cursore accanto al campo **Data di scadenza** e fare doppio clic sulla variabile **Data di scadenza**.
1. Selezionare la scheda **Oggetti modello dati**, posizionare il cursore accanto al campo **Addebito il periodo di fatturazione corrente** nel riquadro a destra, quindi fare doppio clic sulla proprietà **bollette** > **spese d&#39;uso**.

   ![Riepilogo fatturazione](assets/bill_summary_static_variables_new.png)

1. Fare clic su **Salva** per creare il frammento del documento di testo Dettagli cliente.

## Passaggio 4: Crea riepilogo del frammento di documento di testo delle spese {#step-create-summary-of-charges-text-document-fragment}

Il frammento di documento Riepilogo spese include i campi seguenti:

| Campo | Sorgente dati |
|---|---|
| Spese di chiamata | Modello dati modulo |
| Spese di chiamata conferenza | Modello dati modulo |
| Tariffe SMS | Modello dati modulo |
| Tariffe Internet per dispositivi mobili | Modello dati modulo |
| Tariffe di roaming nazionali | Modello dati modulo |
| Tariffe internazionali di roaming | Modello dati modulo |
| Spese per servizi a valore aggiunto | Modello dati modulo |
| Oneri totali | Modello dati modulo |
| TOTALE PAGABILE | Modello dati modulo |

Per creare testo statico e utilizzare gli elementi del modello dati del modulo nel frammento di documento, procedere come segue:

1. Selezionare **[!UICONTROL Forms]** > **[!UICONTROL Frammenti documento]**.
1. Selezionare **Crea** > **Testo**.
1. Specificate le seguenti informazioni:

   1. Immettere **summary_charge_first_ic** come nome nel campo **Title**. Il titolo viene compilato automaticamente nel campo Nome.

   1. Selezionare **Form Data Model** dalla sezione **Data Model**.

   1. Selezionare **FDM_Create_First_IC** come modello dati modulo e toccare **Seleziona**.

   1. Toccare **Next**.

1. Utilizzando il riquadro a destra, potete creare testo statico per i seguenti campi:

   * Spese di chiamata
   * Spese di chiamata conferenza
   * Tariffe SMS
   * Tariffe Internet per dispositivi mobili
   * Tariffe di roaming nazionali
   * Tariffe internazionali di roaming
   * Spese per servizi a valore aggiunto
   * Oneri totali
   * TOTALE PAGABILE

   ![Spese di riepilogo](assets/summary_charges_static_new.png)

1. Selezionare la scheda **Oggetti modello dati**.
1. Posizionare il cursore accanto al campo **Addebiti chiamate** e fare doppio clic sulla proprietà **bollette** > **callcharge**.
1. Posizionare il cursore accanto al campo **Spese di chiamata conferenza** e fare doppio clic sulla proprietà **bollette** > **spese di chiamata conferenza**.
1. Posizionare il cursore accanto al campo **Spese SMS** e fare doppio clic sulla proprietà **bollette** > **smscharges**.
1. Posizionare il cursore accanto al campo **Carica Internet mobile** e fare doppio clic sulla proprietà **bollette** > **internetcharge**.
1. Posizionare il cursore accanto al campo **Tariffe di roaming nazionali** e fare doppio clic sulla proprietà **bollette** > **roaming nazionale**.
1. Posizionare il cursore accanto al campo **Tariffe di roaming internazionale** e fare doppio clic sulla proprietà **bollette** > **roaming**.
1. Posizionare il cursore accanto al campo **Spese per servizi aggiunti** e fare doppio clic sulla proprietà **bollette** > **vas**.
1. Posizionare il cursore accanto al campo **Addebiti totali** e fare doppio clic sulla proprietà **bollette** > **spese d&#39;uso**.
1. Posizionare il cursore accanto al campo **TOTAL PAYABLE** e fare doppio clic sulla proprietà **bollette** > **usagecharge**.

   ![Riepilogo delle spese](assets/summary_charges_static_fdm_new.png)

1. Selezionare il testo nella riga **Spese per servizi aggiunti di valore** e toccare **Crea regola** per creare una condizione in base alla quale la riga viene visualizzata nella comunicazione interattiva:
1. Nella finestra a comparsa **Crea regola**:

   1. Selezionare **Modelli di dati e variabili**, quindi **bollette** > **callcharge**.

   1. Selezionare **è minore di** come operatore.
   1. Selezionare **Number** e immettere il valore come **60**.

   In base a questa condizione, la riga Added Services Added Cost viene visualizzata solo se il valore per il campo Call Addebiti è inferiore a 60.

   ![create_rules_caption](assets/create_rules_caption.gif)

1. Fare clic su **Salva** per creare il frammento di testo Riepilogo delle spese.
