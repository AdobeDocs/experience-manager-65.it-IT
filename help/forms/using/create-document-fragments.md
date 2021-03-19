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
feature: Comunicazione interattiva
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1684'
ht-degree: 2%

---


# Esercitazione: Crea frammenti di documento{#tutorial-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Questa esercitazione è un passaggio della serie [Crea la tua prima comunicazione interattiva](/help/forms/using/create-your-first-interactive-communication.md). Si consiglia di seguire la serie in sequenza cronologica per comprendere, eseguire e illustrare il caso d’uso completo dell’esercitazione.

I frammenti di documento sono componenti riutilizzabili di una corrispondenza utilizzati per comporre una comunicazione interattiva. I frammenti di documento sono di tipo:

* Testo : per risorsa di testo si intende un contenuto costituito da uno o più paragrafi di testo. Un paragrafo può essere statico o dinamico.
* Elenco : elenco è un gruppo di frammenti di documento, inclusi testo, elenchi, condizioni e immagini.
* Condizione : le condizioni ti consentono di definire quale contenuto viene incluso nella comunicazione interattiva in base ai dati ricevuti dal modello dati del modulo.

Questa esercitazione descrive i passaggi necessari per creare più frammenti di documento di testo in base all&#39;anatomia fornita nella sezione [Pianificare la comunicazione interattiva](/help/forms/using/planning-interactive-communications.md) . Al termine di questa esercitazione, potrai:

* Creazione di frammenti di documento
* Creare variabili
* Creare e applicare regole

![text_document_fragments](assets/text_document_fragments.gif)

Di seguito è riportato l’elenco dei frammenti di documento creati in questa esercitazione:

* [Dettagli fattura](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [Dettagli cliente](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [Riepilogo fatture](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [Sommario degli oneri](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

Ogni frammento di documento include campi con testo statico, dati ricevuti dal modello dati del modulo e dati immessi tramite l’interfaccia utente dell’agente. Tutti questi campi sono stati descritti nella sezione [Pianifica la comunicazione interattiva](/help/forms/using/planning-interactive-communications.md) .

Durante la creazione di frammenti di documento in questa esercitazione, vengono create variabili per i campi che ricevono dati tramite l’interfaccia utente dell’agente.

Utilizzare **FDM_Create_First_IC**, come descritto nella sezione [Crea modello dati modulo](../../forms/using/create-form-data-model0.md), come modello dati modulo per creare frammenti di documento in questa esercitazione.

## Passaggio 1: Crea frammento di documento di testo Dettagli fattura {#step-create-bill-details-text-document-fragment}

Il frammento di documento Dettagli fatturazione include i campi seguenti:

| Campo | Sorgente dati |
|---|---|
| Numero fattura | Interfaccia utente agente |
| Periodo fatturazione | Interfaccia utente agente |
| Data fatturazione | Interfaccia utente agente |
| Il tuo piano | Modello dati modulo |

Esegui i seguenti passaggi per creare variabili per i campi con l’interfaccia utente agente come origine dati, creare testo statico e utilizzare elementi modello dati modulo nel frammento di documento:

1. Selezionare **[!UICONTROL Forms]** > **[!UICONTROL Frammenti documento]**.

1. Seleziona **Crea** > **Testo**.
1. Specifica le seguenti informazioni:

   1. Inserisci **bill_details_first_ic** come nome nel campo **Titolo** . Il titolo viene compilato automaticamente nel campo **Nome** .

   1. Seleziona **Modello dati modulo** dalla sezione **Modello dati** .

   1. Seleziona **FDM_Create_First_IC** come modello di dati del modulo e tocca **Seleziona**.

   1. Tocca **Avanti**.

1. Seleziona la scheda **Variabili** nel riquadro a sinistra e tocca **Crea**.
1. Nella sezione **Crea variabile** :

   1. Immetti **Numero di fattura** come nome della variabile.
   1. Selezionare **Stringa** come tipo.
   1. Tocca **Crea**.

   ![Crea variabile di tipo String](assets/variable_create_string_new.png)

   Ripeti i passaggi 4 e 5 per creare le seguenti variabili:

   * Periodo di fatturazione: Tipo di stringa
   * Data fatturazione: Tipo di data

   ![Dettagli fattura](assets/variable_bill_details_new.png)

1. Crea il testo statico per i campi seguenti utilizzando il riquadro di destra:

   * Numero fattura
   * Periodo fatturazione
   * Data fatturazione
   * Il tuo piano

   ![Testo statico](assets/variable_bill_details_static_text_new.png)

1. Posizionare il cursore accanto al campo **Nr. fattura** e fare doppio clic sulla variabile **NumeroFattura** dalla scheda **Variabili** nel riquadro a sinistra.
1. Posizionare il cursore accanto al campo **Periodo di fatturazione** e fare doppio clic sulla variabile **Periodo di fatturazione**.
1. Posizionare il cursore accanto al campo **Data fatturazione** e fare doppio clic sulla variabile **Data fatturazione**.
1. Selezionare la scheda **Oggetti modello dati** nel riquadro a sinistra.
1. Posiziona il cursore accanto al campo **Piano** e fai doppio clic sulla proprietà **cliente** > **customerplan** .

   ![bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. Fare clic su **Salva** per creare il frammento di testo del documento Dettagli fatturazione.

## Passaggio 2: Crea frammento di documento di testo Dettagli cliente {#step-create-customer-details-text-document-fragment}

Il frammento di documento Dettagli cliente include i campi seguenti:

| Campo | Sorgente dati |
|---|---|
| Nome cliente | Modello dati modulo |
| Indirizzo | Modello dati modulo |
| Luogo di fornitura | Interfaccia utente agente |
| Codice di stato | Interfaccia utente agente |
| Numero cellulare | Modello dati modulo |
| Numero di contatto alternativo | Modello dati modulo |
| Numero di relazione | Modello dati modulo |
| Numero di connessioni | Interfaccia utente agente |

Esegui i seguenti passaggi per creare variabili per i campi con l’interfaccia utente agente come origine dati, creare testo statico e utilizzare elementi modello dati modulo nel frammento di documento:

1. Selezionare **[!UICONTROL Forms]** > **[!UICONTROL Frammenti documento]**.
1. Seleziona **Crea** > **Testo**.
1. Specifica le seguenti informazioni:

   1. Immetti **customer_details_first_ic** come nome nel campo **Titolo** . Il titolo viene compilato automaticamente nel campo **Nome** .

   1. Seleziona **Modello dati modulo** dalla sezione **Modello dati** .

   1. Seleziona **FDM_Create_First_IC** come modello di dati del modulo e tocca **Seleziona**.

   1. Tocca **Avanti**.

1. Seleziona la scheda **Variabili** nel riquadro a sinistra e tocca **Crea**.
1. Nella sezione **Crea variabile** :

   1. Immetti **Placesupply** come nome della variabile.
   1. Selezionare **Stringa** come tipo.
   1. Tocca **Crea**.

   Ripeti i passaggi 4 e 5 per creare le seguenti variabili:

   * Codice di stato: Tipo di numero
   * Connessioni numeriche: Tipo di numero


1. Selezionare la scheda **Oggetti modello dati**, posizionare il cursore nel riquadro di destra e fare doppio clic sulla proprietà **customer** > **name** .
1. Premere Invio per spostare il cursore sulla riga successiva e fare doppio clic sulla proprietà **customer** > **address** .
1. Crea il testo statico per i campi seguenti utilizzando il riquadro di destra:

   * Numero cellulare
   * Numero di contatto alternativo
   * Luogo di fornitura
   * Numero di relazione
   * Codice di stato
   * Numero di connessioni

   ![Testo statico dei dettagli del cliente](assets/customer_details_static_text_new.png)

1. Posiziona il cursore accanto al campo **Mobile Number** e fai doppio clic sulla proprietà **customer** > **mobilenum** .
1. Posiziona il cursore accanto al campo **Numero di contatto alternativo** e fai doppio clic sulla proprietà** customer* > **alternatemobilenumber** .
1. Posiziona il cursore accanto al campo **Numero relazione** e fai doppio clic sulla proprietà **cliente** > **numero relazione** .
1. Selezionare la scheda **Variabili**, posizionare il cursore accanto al campo **Luogo di fornitura** e fare doppio clic sulla variabile **Placesupply**.
1. Posiziona il cursore accanto al campo **Codice di stato** e fai doppio clic sulla variabile **Codice di stato** .
1. Posizionare il cursore accanto al campo **Numero di connessioni** e fare doppio clic sulla variabile **Numberconnections**.

   ![Dettagli cliente](assets/customer_details_df2_new.png)

1. Fai clic su **Salva** per creare il frammento di testo del documento Dettagli cliente .

## Passaggio 3: Crea frammento di documento di testo sintetico fattura {#step-create-bill-summary-text-document-fragment}

Il frammento di documento Sintetico distinta include i campi seguenti:

| Campo | Sorgente dati |
|---|---|
| Saldo precedente | Interfaccia utente agente |
| Pagamenti | Interfaccia utente agente |
| Regolazioni | Interfaccia utente agente |
| Addebita il periodo di fatturazione corrente | Modello dati modulo |
| Importo dovuto | Interfaccia utente agente |
| Data di scadenza | Interfaccia utente agente |

Esegui i seguenti passaggi per creare variabili per i campi con l’interfaccia utente agente come origine dati, creare testo statico e utilizzare elementi modello dati modulo nel frammento di documento:

1. Selezionare **[!UICONTROL Forms]** > **[!UICONTROL Frammenti documento]**.
1. Seleziona **Crea** > **Testo**.
1. Specifica le seguenti informazioni:

   1. Inserisci **bill_summary_first_ic** come nome nel campo **Titolo** . Il titolo viene compilato automaticamente nel campo **Nome** .

   1. Seleziona **Modello dati modulo** dalla sezione **Modello dati** .

   1. Seleziona **FDM_Create_First_IC** come modello di dati del modulo e tocca **Seleziona**.

   1. Tocca **Avanti**.

1. Seleziona la scheda **Variabili** nel riquadro a sinistra e tocca **Crea**.
1. Nella sezione **Crea variabile** :

   1. Inserisci **Precedente balance** come nome della variabile.
   1. Selezionare **Number** come tipo.
   1. Tocca **Crea**.

   Ripeti i passaggi 4 e 5 per creare le seguenti variabili:

   * Pagamenti: Tipo di numero
   * Adeguamenti: Tipo di numero
   * Alpinita: Tipo di numero
   * Data di scadenza: Tipo di data


1. Crea il testo statico per i campi seguenti utilizzando il riquadro di destra:

   * Saldo precedente
   * Pagamenti
   * Regolazioni
   * Addebita il periodo di fatturazione corrente
   * Importo dovuto
   * Data di scadenza
   * Le spese di pagamento in ritardo dopo la data di scadenza sono $ 20

   ![Testo statico Riepilogo effetti](assets/bill_summary_static_new.png)

1. Posizionare il cursore accanto al campo **Saldo precedente** e fare doppio clic sulla variabile **Saldo precedente**.
1. Posizionare il cursore accanto al campo **Pagamenti** e fare doppio clic sulla variabile **Pagamenti**.
1. Posizionare il cursore accanto al campo **Regolazioni** e fare doppio clic sulla variabile **Regolazioni**.
1. Posiziona il cursore accanto al campo **Importo dovuto** e fai doppio clic sulla variabile **Allunga**.
1. Posiziona il cursore accanto al campo **Data di scadenza** e fai doppio clic sulla variabile **Duedate** .
1. Selezionare la scheda **Oggetti modello dati**, posizionare il cursore accanto al campo **Carica il periodo di fatturazione corrente** nel riquadro di destra, quindi fare doppio clic sulla proprietà **bollette** > **usagecariche**.

   ![Riepilogo fatture](assets/bill_summary_static_variables_new.png)

1. Fai clic su **Salva** per creare il frammento di testo del documento Dettagli cliente .

## Passaggio 4: Crea riepilogo del frammento di documento di testo di addebito {#step-create-summary-of-charges-text-document-fragment}

Il frammento di documento Riepilogo delle spese include i campi seguenti:

| Campo | Sorgente dati |
|---|---|
| Spese di chiamata | Modello dati modulo |
| Tariffe di chiamata della conferenza | Modello dati modulo |
| Tariffe SMS | Modello dati modulo |
| Tariffe Internet per dispositivi mobili | Modello dati modulo |
| Tariffe di roaming nazionali | Modello dati modulo |
| Diritti internazionali di roaming | Modello dati modulo |
| Spese per servizi a valore aggiunto | Modello dati modulo |
| Oneri totali | Modello dati modulo |
| TOTALE PAGABILE | Modello dati modulo |

Per creare testo statico e utilizzare gli elementi del modello dati modulo nel frammento di documento, eseguire i seguenti passaggi:

1. Selezionare **[!UICONTROL Forms]** > **[!UICONTROL Frammenti documento]**.
1. Seleziona **Crea** > **Testo**.
1. Specifica le seguenti informazioni:

   1. Inserisci **summary_carts_first_ic** come nome nel campo **Titolo** . Il titolo viene compilato automaticamente nel campo Nome .

   1. Seleziona **Modello dati modulo** dalla sezione **Modello dati** .

   1. Seleziona **FDM_Create_First_IC** come modello di dati del modulo e tocca **Seleziona**.

   1. Tocca **Avanti**.

1. Crea il testo statico per i campi seguenti utilizzando il riquadro di destra:

   * Spese di chiamata
   * Tariffe di chiamata della conferenza
   * Tariffe SMS
   * Tariffe Internet per dispositivi mobili
   * Tariffe di roaming nazionali
   * Diritti internazionali di roaming
   * Spese per servizi a valore aggiunto
   * Oneri totali
   * TOTALE PAGABILE

   ![Spese di riepilogo](assets/summary_charges_static_new.png)

1. Selezionare la scheda **Oggetti modello dati**.
1. Posiziona il cursore accanto al campo **Carica chiamate** e fai doppio clic sulla proprietà **bollette** > **cariche di chiamata** .
1. Posizionare il cursore accanto al campo **Carica chiamate conferenza** e fare doppio clic sulla proprietà **bollette** > **cariche chiamate conferenza** .
1. Posiziona il cursore accanto al campo **Carica SMS** e fai doppio clic sulla proprietà **bollette** > **scharges** .
1. Posiziona il cursore accanto al campo **Carica Internet mobile** e fai doppio clic sulla proprietà **bollette** > **internetcares** .
1. Posizionare il cursore accanto al campo **Tariffe di roaming nazionali** e fare doppio clic sulla proprietà **bollette** > **roaming nazionale** .
1. Posiziona il cursore accanto al campo **Tariffe di roaming internazionali** e fai doppio clic sulla proprietà **bollette** > **roaming** .
1. Posiziona il cursore accanto al campo **Spese per servizi aggiunti** e fai doppio clic sulla proprietà **bollette** > **vas** .
1. Posiziona il cursore accanto al campo **Carica totale** e fai doppio clic sulla proprietà **bollette** > **spese d&#39;uso** .
1. Posizionare il cursore accanto al campo **TOTAL PAYABLE** e fare doppio clic sulla proprietà **bollette** > **usagecariche** .

   ![Sintesi dei costi](assets/summary_charges_static_fdm_new.png)

1. Seleziona il testo nella riga **Costi dei servizi aggiunti** e tocca **Crea regola** per creare una condizione in base alla quale la riga viene visualizzata nella comunicazione interattiva:
1. Nella finestra a comparsa **Crea regola** :

   1. Seleziona **Modelli di dati e variabili**, quindi **bollette** > **callcharge**.

   1. Seleziona **è minore di** come operatore.
   1. Selezionare **Numero** e immettere il valore come **60**.

   In base a questa condizione, la riga Spese per servizi aggiunti valore viene visualizzata solo se il valore del campo Addebiti chiamate è inferiore a 60.

   ![create_rules_caption](assets/create_rules_caption.gif)

1. Fare clic su **Salva** per creare il frammento di testo del riepilogo degli addebiti.
