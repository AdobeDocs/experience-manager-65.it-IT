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
source-git-commit: 709d8fe467f5449eb1e844a49126535a4a4a6e7a

---


# Esercitazione: Creazione di frammenti di documento{#tutorial-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Questa esercitazione è un passaggio della serie [Create your first Interactive Communication](/help/forms/using/create-your-first-interactive-communication.md) (Creazione della prima serie di comunicazioni interattive). Si consiglia di seguire le serie in sequenza cronologica per comprendere, eseguire e dimostrare l&#39;uso completo dell&#39;esercitazione.

I frammenti di documento sono componenti riutilizzabili di una corrispondenza utilizzata per comporre una comunicazione interattiva. I frammenti di documento sono dei tipi seguenti:

* Testo: una risorsa di testo è un contenuto costituito da uno o più paragrafi di testo. Un paragrafo può essere statico o dinamico.
* Elenco - Elenco è un gruppo di frammenti di documento, inclusi testo, elenchi, condizioni e immagini.
* Condizione: le condizioni consentono di definire il contenuto da includere nella comunicazione interattiva in base ai dati ricevuti dal modello dati del modulo.

Questa esercitazione illustra i passaggi necessari per creare più frammenti di documento di testo in base all&#39;anatomia fornita nella sezione [Pianificare la comunicazione](/help/forms/using/planning-interactive-communications.md) interattiva. Al termine di questa esercitazione, potrete:

*  Creazione di frammenti di documento
* Creare variabili
* Creazione e applicazione di regole

![text_document_fragments](assets/text_document_fragments.gif)

Di seguito è riportato l&#39;elenco dei frammenti di documento creati con questa esercitazione:

* [Dettagli fattura](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [Dettagli cliente](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [Riepilogo fatturazione](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [Riepilogo delle spese](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

Ciascun frammento di documento include campi con testo statico, dati ricevuti dal modello dati del modulo e dati immessi tramite l&#39;interfaccia utente dell&#39;agente. Tutti questi campi sono stati rappresentati nella sezione [Pianificare la comunicazione](/help/forms/using/planning-interactive-communications.md) interattiva.

Durante la creazione di frammenti di documento in questa esercitazione, vengono create variabili per i campi che ricevono dati tramite l&#39;interfaccia utente dell&#39;agente.

In questa esercitazione, utilizzare **FDM_Create_First_IC**, come descritto nella sezione [Crea modello](../../forms/using/create-form-data-model0.md) dati modulo, come modello dati modulo per creare frammenti di documento.

## Passaggio 1: Crea frammento di testo Dettagli fatturazione {#step-create-bill-details-text-document-fragment}

Il frammento di documento Dettagli fatturazione include i campi seguenti:

| Campo | Sorgente dati |
|---|---|
| Numero fattura | INTERFACCIA UTENTE agente |
| Periodo fatturazione | INTERFACCIA UTENTE agente |
| Data fatturazione | INTERFACCIA UTENTE agente |
| Il tuo piano | Modello dati modulo |

Per creare variabili per i campi con l’interfaccia utente agente come origine dati, creare testo statico e utilizzare gli elementi del modello dati del modulo nel frammento di documento, procedere come segue:

1. Selezionare **Moduli** > Frammenti **** documento.

1. Selezionare **Crea** > **Testo**.
1. Specificate le seguenti informazioni:

   1. Immettere **bill_details_first_ic** come nome nel campo **Titolo** . Il titolo viene popolato automaticamente nel campo **Nome** .

   1. Selezionare Modello **dati** modulo dalla sezione Modello **** dati.

   1. Selezionare **FDM_Create_First_IC** come modello dati modulo e toccare **Seleziona**.

   1. Toccate **Avanti**.

1. Selezionate la scheda **Variabili** nel riquadro a sinistra e toccate **Crea**.
1. Nella sezione **Crea variabile** :

   1. Immettere il **numero di fattura** come nome della variabile.
   1. Selezionare **Stringa** come tipo.
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

1. Posizionare il cursore accanto al campo **Numero** fattura e fare doppio clic sulla variabile **Numero** fattura dalla scheda **Variabili** nel riquadro a sinistra.
1. Posizionare il cursore accanto al campo **Periodo** fatturazione e fare doppio clic sulla variabile **Periodo** fatturazione.
1. Posizionare il cursore accanto al campo Data **** fattura e fare doppio clic sulla variabile Data **** fattura.
1. Selezionare la scheda Oggetti **modello** dati nel riquadro a sinistra.
1. Posizionare il cursore accanto al campo **Piano** e fare doppio clic sulla proprietà **cliente** > **piano** cliente.

   ![bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. Fare clic su **Salva** per creare il frammento di testo relativo ai dettagli fatture.

## Passaggio 2: Crea frammento di testo Dettagli cliente {#step-create-customer-details-text-document-fragment}

Il frammento di documento Dettagli cliente include i campi seguenti:

| Campo | Sorgente dati |
|---|---|
| Nome cliente | Modello dati modulo |
| Indirizzo | Modello dati modulo |
| Luogo di fornitura | INTERFACCIA UTENTE agente |
| Codice di stato | INTERFACCIA UTENTE agente |
| Numero cellulare | Modello dati modulo |
| Numero di contatto alternativo | Modello dati modulo |
| Numero relazione | Modello dati modulo |
| Numero di connessioni | INTERFACCIA UTENTE agente |

Per creare variabili per i campi con l’interfaccia utente agente come origine dati, creare testo statico e utilizzare gli elementi del modello dati del modulo nel frammento di documento, procedere come segue:

1. Selezionare **Moduli** > Frammenti **** documento.
1. Selezionare **Crea** > **Testo**.
1. Specificate le seguenti informazioni:

   1. Immettete **customer_details_first_ic** come nome nel campo **Titolo** . Il titolo viene popolato automaticamente nel campo **Nome** .

   1. Selezionare Modello **dati** modulo dalla sezione Modello **** dati.

   1. Selezionare **FDM_Create_First_IC** come modello dati modulo e toccare **Seleziona**.

   1. Toccate **Avanti**.

1. Selezionate la scheda **Variabili** nel riquadro a sinistra e toccate **Crea**.
1. Nella sezione **Crea variabile** :

   1. Immettere **Placesupply** come nome della variabile.
   1. Selezionare **Stringa** come tipo.
   1. Toccate **Crea**.
   Ripetere i passaggi 4 e 5 per creare le seguenti variabili:

   * Codice di stato: Tipo di numero
   * Numberconnection: Tipo di numero


1. Selezionare la scheda Oggetti **modello** dati, posizionare il cursore nel riquadro a destra e fare doppio clic sulla proprietà **customer** > **name** .
1. Premere Invio per spostare il cursore sulla riga successiva e fare doppio clic sulla proprietà **customer** > **address** .
1. Utilizzando il riquadro a destra, potete creare testo statico per i seguenti campi:

   * Numero cellulare
   * Numero di contatto alternativo
   * Luogo di fornitura
   * Numero relazione
   * Codice di stato
   * Numero di connessioni
   ![Testo statico dei dettagli del cliente](assets/customer_details_static_text_new.png)

1. Posizionare il cursore accanto al campo Numero **** mobile e fare doppio clic sulla proprietà **customer** > **mobilenum** .
1. Posizionare il cursore accanto al campo Numero **di contatto** alternativo e fare doppio clic sulla proprietà** customer* > **alternatemobilenumber** .
1. Posizionare il cursore accanto al campo Numero **** relazione e fare doppio clic sulla proprietà **cliente** > **Numero** relazione.
1. Selezionare la scheda **Variabili** , posizionare il cursore accanto al campo **Posizione fornitura** e fare doppio clic sulla variabile **Placesupply** .
1. Posizionare il cursore accanto al campo Codice **di** stato e fare doppio clic sulla variabile **Codice** di stato.
1. Posizionare il cursore accanto al campo **Numero di connessioni** e fare doppio clic sulla variabile **Connessioni** numeriche.

   ![Dettagli cliente](assets/customer_details_df2_new.png)

1. Fare clic su **Salva** per creare il frammento di testo del documento Dettagli cliente.

## Passaggio 3: Crea frammento di testo Riepilogo fatturazione {#step-create-bill-summary-text-document-fragment}

Il frammento di documento Riepilogo fatturazione include i campi seguenti:

| Campo | Sorgente dati |
|---|---|
| Saldo precedente | INTERFACCIA UTENTE agente |
| Pagamenti | INTERFACCIA UTENTE agente |
| Regolazioni | INTERFACCIA UTENTE agente |
| Addebito periodo corrente | Modello dati modulo |
| Importo dovuto | INTERFACCIA UTENTE agente |
| Data di scadenza | INTERFACCIA UTENTE agente |

Per creare variabili per i campi con l’interfaccia utente agente come origine dati, creare testo statico e utilizzare gli elementi del modello dati del modulo nel frammento di documento, procedere come segue:

1. Selezionare **Moduli** > Frammenti **** documento.
1. Selezionare **Crea** > **Testo**.
1. Specificate le seguenti informazioni:

   1. Immettere **bill_summary_first_ic** come nome nel campo **Titolo** . Il titolo viene popolato automaticamente nel campo **Nome** .

   1. Selezionare Modello **dati** modulo dalla sezione Modello **** dati.

   1. Selezionare **FDM_Create_First_IC** come modello dati modulo e toccare **Seleziona**.

   1. Toccate **Avanti**.

1. Selezionate la scheda **Variabili** nel riquadro a sinistra e toccate **Crea**.
1. Nella sezione **Crea variabile** :

   1. Immettere **il saldo** precedente come nome della variabile.
   1. Selezionare **Numero** come tipo.
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

1. Posizionare il cursore accanto al campo **Saldo** precedente e fare doppio clic sulla variabile Saldo **** precedente.
1. Posizionare il cursore accanto al campo **Pagamenti** e fare doppio clic sulla variabile **Pagamenti** .
1. Posizionate il cursore accanto al campo **Regolazioni** e fate doppio clic sulla variabile **Regolazioni** .
1. Posizionare il cursore accanto al campo **Importo dovuto** e fare doppio clic sulla variabile **Almontabile** .
1. Posizionare il cursore accanto al campo Data **di** scadenza e fare doppio clic sulla variabile **Data** di scadenza.
1. Selezionare la scheda Oggetti **modello di** dati, posizionare il cursore accanto al campo Periodo **di fatturazione corrente** Addebiti nel riquadro a destra, quindi fare doppio clic sulla **proprietà fatture** > **addebiti** .

   ![Riepilogo fatturazione](assets/bill_summary_static_variables_new.png)

1. Fare clic su **Salva** per creare il frammento di testo del documento Dettagli cliente.

## Passaggio 4: Crea riepilogo del frammento di documento di testo relativo alle spese {#step-create-summary-of-charges-text-document-fragment}

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

1. Selezionare **Moduli** > Frammenti **** documento.
1. Selezionare **Crea** > **Testo**.
1. Specificate le seguenti informazioni:

   1. Immettete **summary_charge_first_ic** come nome nel campo **Titolo** . Il titolo viene compilato automaticamente nel campo Nome.

   1. Selezionare Modello **dati** modulo dalla sezione Modello **** dati.

   1. Selezionare **FDM_Create_First_IC** come modello dati modulo e toccare **Seleziona**.

   1. Toccate **Avanti**.

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

1. Selezionare la scheda Oggetti **modello** dati.
1. Posizionare il cursore accanto al campo **Addebiti** per chiamate e fare doppio clic sulla proprietà **fatture** > **canoni** .
1. Posizionare il cursore accanto al campo **Spese** chiamate conferenza e fare doppio clic sulla proprietà **fatture** > **spese** di chiamata.
1. Posizionare il cursore accanto al campo **Spese** SMS e fare doppio clic sulla proprietà **fatture** > **schemi** .
1. Posizionare il cursore accanto al campo Tariffe **Internet** mobile e fare doppio clic sulla proprietà **fatture** > **internetcharge** .
1. Posizionare il cursore accanto al campo **Tariffe** di roaming nazionali e fare doppio clic sulle **fatture** > Proprietà **nazionale** di roaming.
1. Posizionare il cursore accanto al campo Tariffe **di roaming** internazionali e fare doppio clic sulla proprietà **fatture** > **canone** .
1. Posizionare il cursore accanto al campo **Spese** servizio aggiunto e fare doppio clic sulla proprietà **fatture** > **vas** .
1. Posizionare il cursore accanto al campo **Addebiti** totali e fare doppio clic sulla proprietà **fatture** > **spese** d&#39;uso.
1. Posizionare il cursore accanto al campo **TOTAL PAYABLE** e fare doppio clic sulla proprietà **bill** > **usagecharge** .

   ![Riepilogo delle spese](assets/summary_charges_static_fdm_new.png)

1. Selezionate il testo nella riga **Spese** servizio aggiunto e toccate **Crea regola** per creare una condizione in base alla quale la riga viene visualizzata nella comunicazione interattiva:
1. Nella finestra a comparsa **Crea regola** :

   1. Selezionare Modelli **dati e variabili** , quindi **fatture** > **callcharge**.

   1. Select **è minore** dell&#39;operatore.
   1. Selezionate **Numero** e immettete il valore come **60**.
   In base a questa condizione, la riga Added Services Added Cost viene visualizzata solo se il valore del campo Call Addebiti è inferiore a 60.

   ![create_rules_caption](assets/create_rules_caption.gif)

1. Fare clic su **Salva** per creare il frammento di testo Riepilogo spese.
