---
title: "Esercitazione: Crea comunicazione interattiva "
seo-title: Create an Interactive Communication for Print and Web
description: Creare una comunicazione interattiva utilizzando tutti i blocchi predefiniti
seo-description: Create an Interactive Communication using all building blocks
uuid: 5ffaa86f-87c7-4673-8b41-63ec61421be2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ac5d8d4f-fc13-4e8d-819c-c5db07fa6870
docset: aem65
feature: Interactive Communication
exl-id: aaacee66-6bbe-498b-91b1-3a9545ff1aeb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 0%

---

# Esercitazione: Creazione di comunicazioni interattive {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

Questa esercitazione è un passaggio nel [Creare la prima comunicazione interattiva](/help/forms/using/create-your-first-interactive-communication.md) serie. Si consiglia di seguire la serie in sequenza cronologica per comprendere, eseguire e illustrare il caso d’uso completo dell’esercitazione.

Dopo aver creato tutti i blocchi predefiniti, ad esempio il modello dati del modulo, i frammenti di documento, i modelli e i temi per la versione web, puoi iniziare a creare una comunicazione interattiva.

Le comunicazioni interattive possono essere trasmesse attraverso due canali: Stampa e Web. È inoltre possibile creare una comunicazione interattiva con il canale Stampa come principale. L&#39;opzione Stampa come master per il canale Web assicura che il contenuto, l&#39;ereditarietà e il binding dei dati del canale Web siano derivati dal canale Stampa. Inoltre, assicura che le modifiche apportate nel canale Stampa siano sincronizzate nel canale Web. Gli autori delle comunicazioni interattive possono tuttavia interrompere l’ereditarietà di componenti specifici nel canale Web.

Questa esercitazione illustra i passaggi necessari per creare comunicazioni interattive per i canali Stampa e Web. Al termine di questa esercitazione, potrai:

* Creazione di comunicazioni interattive per il canale di stampa
* Creare comunicazioni interattive per il canale web
* Creazione di comunicazioni interattive per la stampa e il web con Stampa come principale

## Creazione di comunicazioni interattive per la stampa e il Web senza sincronizzazione {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### Creare comunicazioni interattive per il canale di stampa {#create-interactive-communication-for-print-channel}

Di seguito è riportato l’elenco delle risorse già create in questa esercitazione e necessarie durante la creazione della comunicazione interattiva per il canale Stampa:

**Modello di stampa:** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**Modello dati modulo:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Frammenti documento:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charge_first_ic](../../forms/using/create-document-fragments.md)

**Frammenti di layout:** [table_lf](../../forms/using/create-templates-print-web.md)

**Immagini:** PayNow e ValueAddedServices

1. Accedi all&#39;istanza di authoring AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Tocca **Crea** e seleziona **Comunicazione interattiva**. La **Creazione di comunicazioni interattive** viene visualizzata la procedura guidata.
1. Specifica **create_first_ic** in **Titolo** e **Nome** campo . Seleziona **FDM_Create_First_IC** come modello dati modulo e tocca **Successivo**.
1. In **Canali** procedura guidata:

   1. Specifica **create_first_ic_print_template** come modello di stampa e tocca **Seleziona**. Assicurati che **Usa Stampa come master per il canale web** casella di controllo non selezionata.

   1. Specifica **Crea_First_IC_templates** cartella > **Crea_Primo_IC_Modello_Web** come modello web e tocca **Seleziona**.

   1. Tocca **Crea**.

   Viene visualizzato un messaggio di conferma della corretta creazione della comunicazione interattiva.

1. Tocca **Modifica** per aprire la comunicazione interattiva nel riquadro a destra.
1. Vai a **Risorse** e applicare il filtro per visualizzare solo i frammenti di documento nel riquadro a sinistra.
1. Trascina e rilascia i seguenti frammenti di documento nelle aree di destinazione nella comunicazione interattiva:

   | Frammento di documento | Area di destinazione |
   |---|---|
   | bill_details_first_ic | DettagliFattura |
   | customer_details_first_ic | DettagliCliente |
   | bill_summary_first_ic | RiepilogoFatturazione |
   | summary_charge_first_interinterattivo_communication | Oneri |

   ![Frammenti di documenti per le comunicazioni interattive](assets/create_first_ic_doc_fragments_new.png)

1. Tocca **Grafici** area di destinazione e tocca **+** per aggiungere un **Grafico** componente.
1. Tocca il componente Grafico e seleziona ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà del grafico vengono visualizzate nel riquadro a sinistra:

   1. Specifica un nome per il grafico.
   1. Seleziona **Torta** dal **Tipo di grafico** elenco a discesa.
   1. Seleziona la **calltype** della proprietà **chiama** tipo di oggetto modello dati nel **Asse X** sezione . Tocca ![done_icon](assets/done_icon.png).
   1. Seleziona **Frequenza** dal **Funzione** elenco a discesa.
   1. Seleziona la **calltype** della proprietà **chiama** tipo di oggetto modello dati nel **Asse Y** sezione . Tocca ![done_icon](assets/done_icon.png).
   1. Tocca ![done_icon](assets/done_icon.png) per salvare le proprietà del grafico.

1. Vai a **Risorse** e applica il filtro per visualizzare solo i frammenti di layout nel riquadro a sinistra. Trascina e rilascia la **table_lf** frammento di layout nel **Chiamate dettagliate** area target.
1. Seleziona il Campo di testo nella sezione **Data** tocca e colonna ![configure_icon](assets/configure_icon.png) (Configura).
1. Seleziona **Oggetto Data Model** dal **Tipo di binding** elenco a discesa e seleziona **chiama** > **calldate**. Tocca ![done_icon](assets/done_icon.png) due volte per salvare le proprietà.

   Allo stesso modo, crea un binding con **calltime**, **numero di telefono**, **callduration** e **chiamate** per i campi di testo nella **Time**, **Numero**, **Durata** e **Oneri** rispettivamente.

1. Tocca **PayNow** area di destinazione e tocca **+** per aggiungere un **Immagine** componente.
1. Tocca il componente Immagine e seleziona ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà dell’immagine vengono visualizzate nel riquadro a sinistra:

   1. Specifica **PayNow** come nome dell’immagine nel **Nome** campo .
   1. Tocca **Carica**, seleziona l’immagine salvata nel file system locale e tocca **Apri**.
   1. Tocca ![done_icon](assets/done_icon.png) per salvare le proprietà dell’immagine.

1. Ripetere i passaggi 13 e 14 per aggiungere **ValueAddedServices** all&#39;immagine **ValueAddedServices** area target.

### Creare comunicazioni interattive per il canale web {#create-interactive-communication-for-web-channel}

Di seguito è riportato l’elenco delle risorse già create in questa esercitazione e necessarie durante la creazione della comunicazione interattiva per il canale Web:

**Modello Web:** [Crea_Primo_IC_Modello_Web](../../forms/using/create-templates-print-web.md)

**Modello dati modulo:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Frammenti documento:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charge_first_ic](../../forms/using/create-document-fragments.md)

**Immagini:** PayNowWeb e ValueAddedServicesWeb

1. Accedi all&#39;istanza di authoring AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Tocca **Crea** e seleziona **Comunicazione interattiva**. La **Creazione di comunicazioni interattive** viene visualizzata la procedura guidata.
1. Specifica **create_first_ic** in **Titolo** e **Nome** campo . Seleziona **FDM_Create_First_IC** come modello dati modulo e tocca **Successivo**.
1. In **Canali** procedura guidata:

   1. Specifica **create_first_ic_print_template** come modello di stampa e tocca **Seleziona**. Assicurati che **Usa Stampa come master per il canale web** casella di controllo non selezionata.

   1. Specifica **Crea_First_IC_templates** cartella > **Crea_Primo_IC_Modello_Web** come modello web e tocca **Seleziona**.

   1. Tocca **Crea**.

   Viene visualizzato un messaggio di conferma della corretta creazione della comunicazione interattiva.

1. Tocca **Modifica** per aprire la comunicazione interattiva nel riquadro a destra.
1. Tocca **Canali** dal riquadro a sinistra e tocca **Web**.
1. Vai a **Risorse** e applicare il filtro per visualizzare solo i frammenti di documento nel riquadro a sinistra.
1. Trascina e rilascia i seguenti frammenti di documento nelle aree di destinazione nella comunicazione interattiva:

   | Frammento di documento | Area di destinazione |
   |---|---|
   | bill_details_first_ic | DettagliFattura |
   | customer_details_first_ic | DettagliCliente |
   | bill_summary_first_ic | RiepilogoFatturazione |
   | summary_charge_first_interinterattivo_communication | Oneri |

1. Tocca **Sintesi dei costi** area di destinazione e tocca **+** per aggiungere un **Grafico** componente.
1. Tocca il componente Grafico e seleziona ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà del grafico vengono visualizzate nel riquadro a sinistra:

   1. Specifica un nome per il grafico.
   1. Seleziona **Torta** dal **Tipo di grafico** elenco a discesa.

   1. Seleziona la **calltype** della proprietà **chiama** tipo di oggetto modello dati nel **Asse X** sezione . Tocca ![done_icon](assets/done_icon.png).

   1. Seleziona **Frequenza** dal **Funzione** elenco a discesa.

   1. Seleziona la **calltype** della proprietà **chiama** tipo di oggetto modello dati nel **Asse Y** sezione . Tocca ![done_icon](assets/done_icon.png).

   1. Tocca ![done_icon](assets/done_icon.png) per salvare le proprietà del grafico.

1. Seleziona la **Origini dati** dal riquadro a sinistra e trascina **chiama** oggetto del modello dati **Chiamate dettagliate** area target. Tutte le proprietà nel **chiama** l&#39;oggetto modello dati viene visualizzato come colonne di tabella nel **Chiamate dettagliate** area di destinazione nel riquadro a destra.

   In base al caso d’uso, nella tabella sono necessarie le colonne Data chiamata, Ora chiamata, Numero chiamata, Durata chiamata e Addebiti chiamata .

   ![Tabella per la comunicazione interattiva](assets/table_ic_web_new.png)

1. Seleziona **Mobilenum** intestazione di colonna della tabella e seleziona **Altre opzioni** > **Elimina colonna**. Allo stesso modo, elimina **Calltype** colonna.
1. Seleziona la **Calldate** intestazione della colonna della tabella e tocca ![modifica](assets/edit.png) (Modifica) per rinominare il testo in **Data chiamata**. Allo stesso modo, rinominare le altre intestazioni di colonna nella tabella.
1. In base al caso d’uso, inserisci un **Paga ora** nella comunicazione interattiva che offre all’utente un’opzione per effettuare il pagamento facendo clic sul pulsante . Esegui i seguenti passaggi per inserire il pulsante:

   1. Tocca **Paga ora** area di destinazione e tocca **+** per aggiungere un **Testo** componente.

   1. Tocca il componente testo e tocca ![modifica](assets/edit.png) (Modifica).
   1. Rinomina il testo in **Paga ora**.
   1. Selezionare il testo e toccare l’icona Collegamento ipertestuale.
   1. Specifica l’URL di pagamento nel **Percorso** campo .
   1. Seleziona **Nuova scheda** da **Target** elenco a discesa.

   1. Tocca ![done_icon](assets/done_icon.png) per salvare le proprietà del collegamento ipertestuale.

1. Seleziona **Stile** dall’elenco a discesa accanto a **Anteprima** opzione .

   ![Modalità Seleziona stile per la comunicazione interattiva](assets/select_style_ic_web_new.png)

1. Definire lo stile del testo del collegamento ipertestuale per visualizzarlo come pulsante nella comunicazione interattiva, eseguendo le operazioni seguenti:

   1. Tocca il componente testo e seleziona ![modifica](assets/edit.png) (Modifica).
   1. In **Bordo** sezione , specifica **1,5 px** come **Larghezza bordo**, seleziona **Uniforme** come **Stile bordo** e specifica **46 px** come **Raggio bordo**.

   1. Seleziona Rosso come colore di sfondo per il pulsante dal **Sfondo** sezione .
   1. In **Margine** campo per **Dimension e posizione** , tocca **Modifica simultaneamente** e imposta la **Destra** margine **450 px**. I campi In alto, In basso e A sinistra sono impostati come vuoti.

   ![Inserire un collegamento ipertestuale nella comunicazione interattiva](assets/ic_web_hyperlink_new.png)

1. Tocca **Paga ora** area di destinazione e tocca **+** per aggiungere un **Immagine** componente.
1. Tocca il componente Immagine e seleziona ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà dell’immagine vengono visualizzate nel riquadro a sinistra:

   1. Specifica **PayNow** come nome dell’immagine nel **Nome** campo .

   1. Tocca **Carica**, seleziona **PayNowWeb** immagine salvata nel file system locale e toccare **Apri**.

   1. Tocca ![done_icon](assets/done_icon.png) per salvare le proprietà dell’immagine.

1. In base al caso d’uso, inserisci un **Abbonati** nella comunicazione interattiva che offre all’utente un’opzione per abbonarsi ai servizi a valore aggiunto facendo clic sul pulsante .

   Ripeti i passaggi 13-17 per aggiungere un **Abbonati** al pulsante **Servizi a valore aggiunto** area di destinazione e aggiungi la **ValueAddedServicesWeb** immagine.

## Creazione di comunicazioni interattive per la stampa e il Web con sincronizzazione automatica {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

È inoltre possibile creare una comunicazione interattiva abilitando la sincronizzazione automatica tra i canali Stampa e Web. Per abilitare la sincronizzazione automatica, selezionare l’opzione Stampa come master durante la creazione della comunicazione interattiva. Selezionando l&#39;opzione Stampa come master, il contenuto, l&#39;ereditarietà e il binding dei dati del canale Web vengono derivati dal canale Stampa. Inoltre, assicura che le modifiche apportate nel canale Stampa si riflettano nel canale Web.

Esegui i seguenti passaggi per derivare il contenuto del canale Web utilizzando il canale Stampa:

1. Accedi all&#39;istanza di authoring AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Tocca **Crea** e seleziona **Comunicazione interattiva**. La **Creazione di comunicazioni interattive** viene visualizzata la procedura guidata.
1. Specifica **create_first_ic** in **Titolo** e **Nome** campo . Seleziona **FDM_Create_First_IC** come modello dati modulo e tocca **Successivo**.
1. In **Canali** procedura guidata:

   1. Specifica **create_first_ic_print_template** come modello di stampa e tocca **Seleziona**.

   1. Seleziona la **Usa Stampa come master per il canale web** casella di controllo.
   1. Specifica **Crea_First_IC_templates** cartella > **Crea_Primo_IC_Modello_Web** come modello web e tocca **Seleziona**.

   1. Tocca **Crea**.

   Viene visualizzato un messaggio di conferma della corretta creazione della comunicazione interattiva.

1. Tocca **Modifica** per aprire la comunicazione interattiva nel riquadro a destra.
1. Esegui i passaggi 6 - 15 di [Creare comunicazioni interattive per il canale di stampa](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel) sezione .
1. Tocca **Canali** dal riquadro a sinistra e tocca **Web** per generare automaticamente il contenuto per il canale Web dal canale Stampa.
1. Come **Usa Stampa come master per il canale web** la casella di controllo è selezionata al passaggio 4, il contenuto e i binding vengono generati automaticamente per il canale Web dal canale Stampa.

   Il contenuto del canale di stampa viene inserito sotto il contenuto del modello del canale Web. Per modificare il contenuto del canale Web generato automaticamente dal canale Stampa, è possibile annullare l&#39;ereditarietà per qualsiasi area di destinazione.

   Passa il puntatore del mouse sull&#39;area di destinazione desiderata nel canale web e seleziona ![annullamento ereditarietà](assets/cancelinheritance.png) (Annulla ereditarietà) e quindi nel **Annulla ereditarietà** finestra di dialogo, tocca **Sì**.

   ![Annulla ereditarietà](assets/cancel_inheritance_web_channel_new.png)

   Se hai annullato l’ereditarietà di un componente, puoi riabilitarlo. Per riabilitare l’ereditarietà, passa il cursore del mouse sul bordo dell’area di destinazione rilevante, che include il componente, e tocca ![reenableeredità](assets/reenableinheritance.png).

1. Seleziona la **Contenuto** nel riquadro a sinistra.
1. Trascina e rilascia il contenuto del canale Web generato automaticamente nei pannelli esistenti nel modello Web utilizzando la struttura del contenuto. Di seguito è riportato l’elenco dei componenti che devono essere ridisposti:

   * Componente Dettagli fatturazione nel pannello Dettagli fatturazione
   * Componente Dettagli cliente al pannello Dettagli cliente
   * Componente Sintetico fatturazione nel pannello Sintetico fatturazione
   * Riepilogo del componente Addebiti al pannello Riepilogo delle spese
   * Frammento di layout (tabella) nel pannello Chiamate dettagliate

   ![Struttura contenuto web](assets/ic_web_content_tree_new.png)

1. Ripeti i passaggi 13 - 18 di [Creare comunicazioni interattive per il canale web](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) per inserire **Paga ora** e **Abbonati** collegamenti ipertestuali nel canale Web della comunicazione interattiva.
