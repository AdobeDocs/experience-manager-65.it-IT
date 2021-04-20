---
title: '"Esercitazione: Crea comunicazione interattiva "'
seo-title: Creazione di una comunicazione interattiva per la stampa e il web
description: Creare una comunicazione interattiva utilizzando tutti i blocchi predefiniti
seo-description: Creare una comunicazione interattiva utilizzando tutti i blocchi predefiniti
uuid: 5ffaa86f-87c7-4673-8b41-63ec61421be2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ac5d8d4f-fc13-4e8d-819c-c5db07fa6870
docset: aem65
feature: Interactive Communication
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 0%

---


# Esercitazione: Crea comunicazione interattiva {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

Questa esercitazione è un passaggio della serie [Crea la tua prima comunicazione interattiva](/help/forms/using/create-your-first-interactive-communication.md). Si consiglia di seguire la serie in sequenza cronologica per comprendere, eseguire e illustrare il caso d’uso completo dell’esercitazione.

Dopo aver creato tutti i blocchi predefiniti, ad esempio il modello dati del modulo, i frammenti di documento, i modelli e i temi per la versione web, puoi iniziare a creare una comunicazione interattiva.

Le comunicazioni interattive possono essere trasmesse attraverso due canali: Stampa e Web. È inoltre possibile creare una comunicazione interattiva con il canale Stampa come principale. L&#39;opzione Stampa come master per il canale Web assicura che il contenuto, l&#39;ereditarietà e il binding dei dati del canale Web siano derivati dal canale Stampa. Inoltre, assicura che le modifiche apportate nel canale Stampa siano sincronizzate nel canale Web. Gli autori delle comunicazioni interattive possono tuttavia interrompere l’ereditarietà di componenti specifici nel canale Web.

Questa esercitazione illustra i passaggi necessari per creare comunicazioni interattive per i canali Stampa e Web. Al termine di questa esercitazione, potrai:

* Creazione di comunicazioni interattive per il canale di stampa
* Creare comunicazioni interattive per il canale web
* Creazione di comunicazioni interattive per la stampa e il web con Stampa come principale

## Creare comunicazioni interattive per la stampa e il Web senza sincronizzazione {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### Creazione di comunicazioni interattive per il canale di stampa {#create-interactive-communication-for-print-channel}

Di seguito è riportato l’elenco delle risorse già create in questa esercitazione e necessarie durante la creazione della comunicazione interattiva per il canale Stampa:

**Modello di stampa:** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**Modello dati modulo:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Frammenti documento:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charge_first_ic](../../forms/using/create-document-fragments.md)

**Frammenti di layout:** [table_lf](../../forms/using/create-templates-print-web.md)

**Immagini:** PayNow e ValueAddedServices

1. Accedi all&#39;istanza di authoring AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Tocca **Crea** e seleziona **Comunicazione interattiva**. Viene visualizzata la procedura guidata **Crea comunicazione interattiva** .
1. Specifica **create_first_ic** nel campo **Titolo** e nel campo **Nome**. Seleziona **FDM_Create_First_IC** come modello dati modulo e tocca **Avanti**.
1. Nella procedura guidata **Canali** :

   1. Specifica **create_first_ic_print_template** come modello di stampa e tocca **Seleziona**. Assicurati che la casella di controllo **Usa stampa come master per il canale Web** non sia selezionata.

   1. Specifica la cartella **Create_First_IC_templates** > **Create_First_IC_Web_Template** come modello Web e tocca **Select**.

   1. Tocca **Crea**.

   Viene visualizzato un messaggio di conferma della corretta creazione della comunicazione interattiva.

1. Tocca **Modifica** per aprire la comunicazione interattiva nel riquadro a destra.
1. Passa alla scheda **Risorse** e applica il filtro per visualizzare solo i frammenti di documento nel riquadro a sinistra.
1. Trascina e rilascia i seguenti frammenti di documento nelle aree di destinazione nella comunicazione interattiva:

   | Frammento di documento | Area di destinazione |
   |---|---|
   | bill_details_first_ic | DettagliFattura |
   | customer_details_first_ic | DettagliCliente |
   | bill_summary_first_ic | RiepilogoFatturazione |
   | summary_charge_first_interinterattivo_communication | Oneri |

   ![Frammenti di documenti per le comunicazioni interattive](assets/create_first_ic_doc_fragments_new.png)

1. Tocca **Grafici** area di destinazione e tocca **+** per aggiungere un componente **Grafico**.
1. Tocca il componente Grafico e seleziona ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà del grafico vengono visualizzate nel riquadro a sinistra:

   1. Specifica un nome per il grafico.
   1. Selezionare **Torta** dall&#39;elenco a discesa **Tipo di grafico**.
   1. Seleziona la proprietà **calltype** dal tipo di oggetto del modello dati **chiama** nella sezione **Asse X** . Tocca ![done_icon](assets/done_icon.png).
   1. Selezionare **Frequenza** dall&#39;elenco a discesa **Funzione**.
   1. Selezionare la proprietà **calltype** dal tipo di oggetto modello dati **chiama** nella sezione **Asse Y**. Tocca ![done_icon](assets/done_icon.png).
   1. Tocca ![done_icon](assets/done_icon.png) per salvare le proprietà del grafico.

1. Passa alla scheda **Risorse** e applica il filtro per visualizzare solo i frammenti di layout nel riquadro a sinistra. Trascina il frammento di layout **table_lf** nell&#39;area di destinazione **Chiamate dettagliate**.
1. Seleziona il Campo di testo nella colonna **Data** e tocca ![configura_icon](assets/configure_icon.png) (Configura).
1. Selezionare **Oggetto modello dati** dall&#39;elenco a discesa **Tipo di binding** e selezionare **chiamate** > **calldate**. Tocca due volte ![done_icon](assets/done_icon.png) per salvare le proprietà.

   Allo stesso modo, crea un binding con **calltime**, **callnumber**, **callduration** e **callcariche** per i campi di testo in **Time**, **Number**, &lt;a12/ Le colonne Duration **e** Carica **rispettivamente.**

1. Tocca **Area target PayNow** e tocca **+** per aggiungere un componente **Immagine**.
1. Tocca il componente Immagine e seleziona ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà dell’immagine vengono visualizzate nel riquadro a sinistra:

   1. Specifica **PayNow** come nome dell&#39;immagine nel campo **Name** .
   1. Tocca **Carica**, seleziona l’immagine salvata nel file system locale e tocca **Apri**.
   1. Tocca ![done_icon](assets/done_icon.png) per salvare le proprietà dell&#39;immagine.

1. Ripetere i passaggi 13 e 14 per aggiungere l&#39;immagine **ValueAddedServices** all&#39;area di destinazione **ValueAddedServices**.

### Creare comunicazioni interattive per il canale web {#create-interactive-communication-for-web-channel}

Di seguito è riportato l’elenco delle risorse già create in questa esercitazione e necessarie durante la creazione della comunicazione interattiva per il canale Web:

**Modello web:** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**Modello dati modulo:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Frammenti documento:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charge_first_ic](../../forms/using/create-document-fragments.md)

**Immagini:** PayNowWeb e ValueAddedServicesWeb

1. Accedi all&#39;istanza di authoring AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Tocca **Crea** e seleziona **Comunicazione interattiva**. Viene visualizzata la procedura guidata **Crea comunicazione interattiva** .
1. Specifica **create_first_ic** nel campo **Titolo** e nel campo **Nome**. Seleziona **FDM_Create_First_IC** come modello dati modulo e tocca **Avanti**.
1. Nella procedura guidata **Canali** :

   1. Specifica **create_first_ic_print_template** come modello di stampa e tocca **Seleziona**. Assicurati che la casella di controllo **Usa stampa come master per il canale Web** non sia selezionata.

   1. Specifica la cartella **Create_First_IC_templates** > **Create_First_IC_Web_Template** come modello Web e tocca **Select**.

   1. Tocca **Crea**.

   Viene visualizzato un messaggio di conferma della corretta creazione della comunicazione interattiva.

1. Tocca **Modifica** per aprire la comunicazione interattiva nel riquadro a destra.
1. Tocca la scheda **Canali** dal riquadro a sinistra e tocca **Web**.
1. Passa alla scheda **Risorse** e applica il filtro per visualizzare solo i frammenti di documento nel riquadro a sinistra.
1. Trascina e rilascia i seguenti frammenti di documento nelle aree di destinazione nella comunicazione interattiva:

   | Frammento di documento | Area di destinazione |
   |---|---|
   | bill_details_first_ic | DettagliFattura |
   | customer_details_first_ic | DettagliCliente |
   | bill_summary_first_ic | RiepilogoFatturazione |
   | summary_charge_first_interinterattivo_communication | Oneri |

1. Tocca **Riepilogo delle spese** nell’area di destinazione e tocca **+** per aggiungere un componente **Grafico**.
1. Tocca il componente Grafico e seleziona ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà del grafico vengono visualizzate nel riquadro a sinistra:

   1. Specifica un nome per il grafico.
   1. Selezionare **Torta** dall&#39;elenco a discesa **Tipo di grafico**.

   1. Seleziona la proprietà **calltype** dal tipo di oggetto del modello dati **chiama** nella sezione **Asse X** . Tocca ![done_icon](assets/done_icon.png).

   1. Selezionare **Frequenza** dall&#39;elenco a discesa **Funzione**.

   1. Selezionare la proprietà **calltype** dal tipo di oggetto modello dati **chiama** nella sezione **Asse Y**. Tocca ![done_icon](assets/done_icon.png).

   1. Tocca ![done_icon](assets/done_icon.png) per salvare le proprietà del grafico.

1. Seleziona la scheda **Origini dati** dal riquadro a sinistra e trascina l&#39;oggetto modello dati **chiamate** nell&#39;area di destinazione **Chiamate dettagliate**. Tutte le proprietà nell&#39;oggetto modello dati **chiamate** vengono visualizzate come colonne di tabella nell&#39;area di destinazione **Chiamate dettagliate** nel riquadro di destra.

   In base al caso d’uso, nella tabella sono necessarie le colonne Data chiamata, Ora chiamata, Numero chiamata, Durata chiamata e Addebiti chiamata .

   ![Tabella per la comunicazione interattiva](assets/table_ic_web_new.png)

1. Seleziona l&#39;intestazione di colonna della tabella **Mobilenum** e seleziona **Altre opzioni** > **Elimina colonna**. Allo stesso modo, elimina la colonna **Calltype** .
1. Seleziona l&#39;intestazione di colonna della tabella **Data di chiamata** e tocca ![modifica](assets/edit.png) (Modifica) per rinominare il testo in **Data di chiamata**. Allo stesso modo, rinominare le altre intestazioni di colonna nella tabella.
1. In base al caso d’uso, inserire un pulsante **Paga ora** nella comunicazione interattiva che offre all’utente un’opzione per effettuare il pagamento facendo clic sul pulsante . Esegui i seguenti passaggi per inserire il pulsante:

   1. Tocca **Paga ora** l’area di destinazione e tocca **+** per aggiungere un componente **Testo**.

   1. Tocca il componente testo e tocca ![modifica](assets/edit.png) (Modifica).
   1. Rinomina il testo in **Paga ora**.
   1. Selezionare il testo e toccare l’icona Collegamento ipertestuale.
   1. Specifica l&#39;URL di pagamento nel campo **Percorso** .
   1. Seleziona **Nuova scheda** dall&#39;elenco a discesa **Target**.

   1. Tocca ![done_icon](assets/done_icon.png) per salvare le proprietà dei collegamenti ipertestuali.

1. Seleziona **Stile** dall&#39;elenco a discesa accanto all&#39;opzione **Anteprima**.

   ![Modalità Seleziona stile per la comunicazione interattiva](assets/select_style_ic_web_new.png)

1. Definire lo stile del testo del collegamento ipertestuale per visualizzarlo come pulsante nella comunicazione interattiva, eseguendo le operazioni seguenti:

   1. Tocca il componente testo e seleziona ![modifica](assets/edit.png) (Modifica).
   1. Nella sezione **Bordo**, specifica **1.5px** come **Larghezza bordo**, seleziona **Solido** come **Stile bordo** e specifica **46px** come &lt;a1 2/>Raggio bordo **.**

   1. Selezionare Rosso come colore di sfondo per il pulsante dalla sezione **Sfondo**.
   1. Nel campo **Margine** per **Dimension e posizione**, tocca l&#39;icona **Modifica simultaneamente** e imposta il margine **Destra** come **450px**. I campi In alto, In basso e A sinistra sono impostati come vuoti.

   ![Inserire un collegamento ipertestuale nella comunicazione interattiva](assets/ic_web_hyperlink_new.png)

1. Tocca **Paga ora** l’area di destinazione e tocca **+** per aggiungere un componente **Immagine**.
1. Tocca il componente Immagine e seleziona ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà dell’immagine vengono visualizzate nel riquadro a sinistra:

   1. Specifica **PayNow** come nome dell&#39;immagine nel campo **Name** .

   1. Tocca **Carica**, seleziona l&#39;immagine **PayNowWeb** salvata sul file system locale, quindi tocca **Apri**.

   1. Tocca ![done_icon](assets/done_icon.png) per salvare le proprietà dell&#39;immagine.

1. In base al caso d’uso, inserisci un pulsante **Sottoscrivi** nella comunicazione interattiva che offre all’utente l’opzione di abbonarsi ai servizi a valore aggiunto facendo clic sul pulsante .

   Ripeti i passaggi 13 - 17 per aggiungere un pulsante **Iscriviti** all&#39;area di destinazione **Servizi aggiunti** e aggiungere l&#39;immagine **ValueAddedServicesWeb**.

## Creazione di comunicazioni interattive per la stampa e il Web con sincronizzazione automatica {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

È inoltre possibile creare una comunicazione interattiva abilitando la sincronizzazione automatica tra i canali Stampa e Web. Per abilitare la sincronizzazione automatica, selezionare l’opzione Stampa come master durante la creazione della comunicazione interattiva. Selezionando l&#39;opzione Stampa come master, il contenuto, l&#39;ereditarietà e il binding dei dati del canale Web vengono derivati dal canale Stampa. Inoltre, assicura che le modifiche apportate nel canale Stampa si riflettano nel canale Web.

Esegui i seguenti passaggi per derivare il contenuto del canale Web utilizzando il canale Stampa:

1. Accedi all&#39;istanza di authoring AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Tocca **Crea** e seleziona **Comunicazione interattiva**. Viene visualizzata la procedura guidata **Crea comunicazione interattiva** .
1. Specifica **create_first_ic** nel campo **Titolo** e nel campo **Nome**. Seleziona **FDM_Create_First_IC** come modello dati modulo e tocca **Avanti**.
1. Nella procedura guidata **Canali** :

   1. Specifica **create_first_ic_print_template** come modello di stampa e tocca **Seleziona**.

   1. Selezionare la casella di controllo **Usa stampa come master per il canale Web**.
   1. Specifica la cartella **Create_First_IC_templates** > **Create_First_IC_Web_Template** come modello Web e tocca **Select**.

   1. Tocca **Crea**.

   Viene visualizzato un messaggio di conferma della corretta creazione della comunicazione interattiva.

1. Tocca **Modifica** per aprire la comunicazione interattiva nel riquadro a destra.
1. Esegui i passaggi 6 - 15 della sezione [Crea comunicazione interattiva per il canale di stampa](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel) .
1. Tocca la scheda **Canali** dal riquadro a sinistra e tocca **Web** per generare automaticamente il contenuto per il canale Web dal canale Stampa.
1. Poiché la casella di controllo **Usa stampa come master per il canale Web** è selezionata al passaggio 4, il contenuto e i binding vengono generati automaticamente per il canale Web dal canale Stampa.

   Il contenuto del canale di stampa viene inserito sotto il contenuto del modello del canale Web. Per modificare il contenuto del canale Web generato automaticamente dal canale Stampa, è possibile annullare l&#39;ereditarietà per qualsiasi area di destinazione.

   Passa il puntatore del mouse sull&#39;area di destinazione desiderata nel canale web e seleziona ![cancelinheritance](assets/cancelinheritance.png) (Annulla ereditarietà), quindi nella finestra di dialogo **Annulla ereditarietà** tocca **Sì**.

   ![Annulla ereditarietà](assets/cancel_inheritance_web_channel_new.png)

   Se hai annullato l’ereditarietà di un componente, puoi riabilitarlo. Per riabilitare l’ereditarietà, passa il cursore del mouse sul bordo dell’area di destinazione rilevante, che include il componente, e tocca ![reenableinheritance](assets/reenableinheritance.png).

1. Seleziona la scheda **Contenuto** nel riquadro a sinistra.
1. Trascina e rilascia il contenuto del canale Web generato automaticamente nei pannelli esistenti nel modello Web utilizzando la struttura del contenuto. Di seguito è riportato l’elenco dei componenti che devono essere ridisposti:

   * Componente Dettagli fatturazione nel pannello Dettagli fatturazione
   * Componente Dettagli cliente al pannello Dettagli cliente
   * Componente Sintetico fatturazione nel pannello Sintetico fatturazione
   * Riepilogo del componente Addebiti al pannello Riepilogo delle spese
   * Frammento di layout (tabella) nel pannello Chiamate dettagliate

   ![Struttura contenuto web](assets/ic_web_content_tree_new.png)

1. Ripetere i passaggi 13 - 18 di [Crea comunicazione interattiva per il canale Web](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) per inserire i collegamenti ipertestuali **Paga ora** e **Iscriviti** nel canale Web della comunicazione interattiva.

