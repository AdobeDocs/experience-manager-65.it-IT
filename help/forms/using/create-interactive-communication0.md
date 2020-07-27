---
title: '"Esercitazione: Crea comunicazione interattiva "'
seo-title: Creazione di una comunicazione interattiva per la stampa e il Web
description: Creazione di una comunicazione interattiva con tutti i blocchi di generazione
seo-description: Creazione di una comunicazione interattiva con tutti i blocchi di generazione
uuid: 5ffaa86f-87c7-4673-8b41-63ec61421be2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ac5d8d4f-fc13-4e8d-819c-c5db07fa6870
docset: aem65
translation-type: tm+mt
source-git-commit: bd70508b361ac8b62ebc0344538a18369a075f3e
workflow-type: tm+mt
source-wordcount: '2020'
ht-degree: 0%

---


# Esercitazione: Creazione di comunicazioni interattive {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

Questa esercitazione è un passaggio della serie [Create your first Interactive Communication](/help/forms/using/create-your-first-interactive-communication.md) (Creazione della prima serie di comunicazioni interattive). Si consiglia di seguire le serie in sequenza cronologica per comprendere, eseguire e dimostrare l&#39;uso completo dell&#39;esercitazione.

Dopo aver creato tutti i blocchi costitutivi come il modello dati del modulo, i frammenti di documento, i modelli e i temi per la versione Web, è possibile iniziare a creare una comunicazione interattiva.

Le comunicazioni interattive possono essere distribuite attraverso due canali: Stampa e Web. Potete anche creare una comunicazione interattiva con il canale Stampa come principale. L&#39;opzione Stampa come principale per il canale Web garantisce che il contenuto, l&#39;ereditarietà e il binding dei dati del canale Web siano derivati dal canale Stampa. Inoltre, garantisce che le modifiche apportate al canale Stampa siano sincronizzate nel canale Web. Gli autori delle comunicazioni interattive possono tuttavia interrompere l’ereditarietà di componenti specifici nel canale Web.

Questa esercitazione illustra i passaggi necessari per creare comunicazioni interattive per i canali Stampa e Web. Al termine di questa esercitazione, potrete:

* Creazione di comunicazioni interattive per il canale di stampa
* Creazione di comunicazioni interattive per il canale Web
* Creazione di comunicazioni interattive per la stampa e il Web con Stampa come principale

## Creazione di comunicazioni interattive per la stampa e il Web senza sincronizzazione {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### Creazione di comunicazioni interattive per il canale di stampa {#create-interactive-communication-for-print-channel}

Di seguito sono elencate le risorse già create in questa esercitazione e necessarie per la creazione della comunicazione interattiva per il canale di stampa:

**Modello di stampa:** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**Modello dati modulo:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Frammenti del documento:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charge_first_ic](../../forms/using/create-document-fragments.md)

**Frammenti di layout:** [table_lf](../../forms/using/create-templates-print-web.md)

**Immagini:** PayNow e ValueAddedServices

1. Accedete all’istanza di creazione di AEM e andate a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Toccate **Crea** e selezionate Comunicazione **** interattiva. Viene visualizzata la procedura guidata **Crea comunicazione** interattiva.
1. Specificate **create_first_ic** nel campo **Titolo** e **Nome** . Selezionare **FDM_Create_First_IC** come modello dati modulo e toccare **Avanti**.
1. Nella procedura guidata **Canali** :

   1. Specificate **create_first_ic_print_template** come modello di stampa e toccate **Seleziona**. Assicurarsi che la casella di controllo **Usa stampa come master per canale** Web non sia selezionata.

   1. Specificate la cartella **Create_First_IC_templates** > **Create_First_IC_Web_Template** come modello Web e toccate **Seleziona**.

   1. Toccate **Crea**.

   Viene visualizzato un messaggio di conferma della corretta creazione della comunicazione interattiva.

1. Toccate **Modifica** per aprire la comunicazione interattiva nel riquadro a destra.
1. Fare clic sulla scheda **Risorse** e applicare il filtro per visualizzare solo i frammenti del documento nel riquadro a sinistra.
1. Trascinare i seguenti frammenti di documento nelle aree di destinazione della comunicazione interattiva:

   | Frammento di documento | Area di destinazione |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | CustomerDetails |
   | bill_summary_first_ic | BillSummary |
   | summary_charge_first_interactive_communication | Oneri |

   ![Frammenti di documenti per le comunicazioni interattive](assets/create_first_ic_doc_fragments_new.png)

1. Toccate l’area di destinazione **Grafici** e toccate **+** per aggiungere un componente **Grafico** .
1. Toccate il componente Grafico e selezionate ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà del grafico vengono visualizzate nel riquadro a sinistra:

   1. Specifica un nome per il grafico.
   1. Selezionare **Torta** dall&#39;elenco a discesa Tipo **** grafico.
   1. Selezionare la proprietà **calltype** dal tipo di oggetto modello dati **chiamate** nella sezione dell&#39;asse **** X. Toccate ![done_icon](assets/done_icon.png).
   1. Selezionare **Frequenza** dall&#39;elenco a discesa **Funzione** .
   1. Selezionare la proprietà **calltype** dal tipo di oggetto modello dati **chiamate** nella sezione dell&#39;asse **** Y. Toccate ![done_icon](assets/done_icon.png).
   1. Toccate ![done_icon](assets/done_icon.png) per salvare le proprietà del grafico.

1. Vai alla scheda **Risorse** e applica il filtro per visualizzare solo i frammenti di layout nel riquadro a sinistra. Trascinare il frammento di layout **table_lf** nell’area di destinazione Chiamate **** dettagliate.
1. Selezionate il Campo di testo nella colonna **Data** e toccate ![configure_icon](assets/configure_icon.png) (Configura).
1. Selezionare Oggetto **modello** dati dall&#39;elenco a discesa Tipo **di** binding, quindi selezionare **chiamate** > **data** di chiamata. Toccate due volte ![done_icon](assets/done_icon.png) per salvare le proprietà.

   Allo stesso modo, potete creare un binding con **calltime**, **callnumber**, **callterm** e **callcharge** per i campi di testo nelle colonne **Time************** ,Number, Durata, Durata, e Oneridi testo.

1. Toccate l’area di destinazione **PayNow** e toccate **+** per aggiungere un componente **Immagine** .
1. Toccate il componente Immagine e selezionate ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà dell’immagine vengono visualizzate nel riquadro a sinistra:

   1. Specificate **PayNow** come nome dell&#39;immagine nel campo **Nome** .
   1. Toccate **Carica**, selezionate l’immagine salvata nel file system locale e toccate **Apri**.
   1. Toccate ![done_icon](assets/done_icon.png) per salvare le proprietà dell&#39;immagine.

1. Ripetere i passaggi 13 e 14 per aggiungere l&#39;immagine **ValueAddedServices** all&#39;area di destinazione **ValueAddedServices** .

### Create Interactive Communication for Web channel {#create-interactive-communication-for-web-channel}

Di seguito è riportato l&#39;elenco delle risorse già create in questa esercitazione e necessarie per la creazione della comunicazione interattiva per il canale Web:

**Modello Web:** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**Modello dati modulo:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Frammenti del documento:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charge_first_ic](../../forms/using/create-document-fragments.md)

**Immagini:** PayNowWeb e ValueAddedServicesWeb

1. Accedete all’istanza di creazione di AEM e andate a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Toccate **Crea** e selezionate Comunicazione **** interattiva. Viene visualizzata la procedura guidata **Crea comunicazione** interattiva.
1. Specificate **create_first_ic** nel campo **Titolo** e **Nome** . Selezionare **FDM_Create_First_IC** come modello dati modulo e toccare **Avanti**.
1. Nella procedura guidata **Canali** :

   1. Specificate **create_first_ic_print_template** come modello di stampa e toccate **Seleziona**. Assicurarsi che la casella di controllo **Usa stampa come master per canale** Web non sia selezionata.

   1. Specificate la cartella **Create_First_IC_templates** > **Create_First_IC_Web_Template** come modello Web e toccate **Seleziona**.

   1. Toccate **Crea**.

   Viene visualizzato un messaggio di conferma della corretta creazione della comunicazione interattiva.

1. Toccate **Modifica** per aprire la comunicazione interattiva nel riquadro a destra.
1. Toccate la scheda **Canali** dal riquadro a sinistra e toccate **Web**.
1. Fare clic sulla scheda **Risorse** e applicare il filtro per visualizzare solo i frammenti del documento nel riquadro a sinistra.
1. Trascinare i seguenti frammenti di documento nelle aree di destinazione della comunicazione interattiva:

   | Frammento di documento | Area di destinazione |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | CustomerDetails |
   | bill_summary_first_ic | BillSummary |
   | summary_charge_first_interactive_communication | Oneri |

1. Toccate **Riepilogo spese** nell’area di destinazione e toccate **+** per aggiungere un componente **Grafico** .
1. Toccate il componente Grafico e selezionate ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà del grafico vengono visualizzate nel riquadro a sinistra:

   1. Specifica un nome per il grafico.
   1. Selezionare **Torta** dall&#39;elenco a discesa Tipo **** grafico.

   1. Selezionare la proprietà **calltype** dal tipo di oggetto modello dati **chiamate** nella sezione dell&#39;asse **** X. Toccate ![done_icon](assets/done_icon.png).

   1. Selezionare **Frequenza** dall&#39;elenco a discesa **Funzione** .

   1. Selezionare la proprietà **calltype** dal tipo di oggetto modello dati **chiamate** nella sezione dell&#39;asse **** Y. Toccate ![done_icon](assets/done_icon.png).

   1. Toccate ![done_icon](assets/done_icon.png) per salvare le proprietà del grafico.

1. Selezionare la scheda **Origini** dati dal riquadro a sinistra e trascinare l&#39;oggetto modello dati **chiamate** nell&#39;area di destinazione Chiamate **** dettagliate. Tutte le proprietà nell&#39;oggetto modello dati **chiamate** sono visualizzate come colonne di tabella nell&#39;area di destinazione Chiamate **** dettagliate nel riquadro a destra.

   In base al caso d’uso, nella tabella sono necessarie le colonne Data chiamata, Ora chiamata, Numero chiamata, Durata chiamata e Addebito chiamate.

   ![Tabella per la comunicazione interattiva](assets/table_ic_web_new.png)

1. Selezionare l&#39;intestazione di colonna della tabella **Mobilenum** e selezionare **Altre opzioni** > **Elimina colonna**. Analogamente, elimina la colonna **Calltype** .
1. Seleziona l’intestazione di colonna della tabella **Calldate** e tocca ![Modifica](assets/edit.png) (Modifica) per rinominare il testo in Data **chiamata**. Allo stesso modo, rinominare le altre intestazioni di colonna nella tabella.
1. In base al caso di utilizzo, inserire un pulsante **Paga** nella comunicazione interattiva che offre all&#39;utente la possibilità di effettuare il pagamento facendo clic sul pulsante. Per inserire il pulsante, eseguire la procedura seguente:

   1. Toccate **Paga ora** nell’area di destinazione e toccate **+** per aggiungere un componente **Testo** .

   1. Toccate il componente di testo e toccate ![Modifica](assets/edit.png) (Modifica).
   1. Rinominare il testo in **Paga ora**.
   1. Selezionate il testo e toccate l&#39;icona Collegamento ipertestuale.
   1. Specificate l&#39;URL di pagamento nel campo **Percorso** .
   1. Selezionare **Nuova scheda** dall&#39;elenco a discesa **Target** .

   1. Toccate ![done_icon](assets/done_icon.png) per salvare le proprietà del collegamento ipertestuale.

1. Selezionare **Stile** dall&#39;elenco a discesa accanto all&#39;opzione **Anteprima** .

   ![Selezionare la modalità Stile per la comunicazione interattiva](assets/select_style_ic_web_new.png)

1. Per formattare il testo del collegamento ipertestuale in modo da visualizzarlo come pulsante nella comunicazione interattiva, procedere come segue:

   1. Toccate il componente di testo e selezionate ![Modifica](assets/edit.png) (Modifica).
   1. Nella sezione **Bordo** , specificate **1,5px** come Larghezza **** bordo, selezionate **Uniforme** come Stile ******** **** bordo e specificate46pxcome raggio di bordo fisso.

   1. Selezionate Rosso come colore di sfondo per il pulsante dalla sezione **Sfondo** .
   1. Nel campo **Margine** per **Dimensioni e posizione** , toccate l’icona **Modifica simultaneamente** e impostate il margine **destro** su **450 pixel**. I campi In alto, In basso e A sinistra sono impostati come vuoti.

   ![Inserisci collegamento ipertestuale nella comunicazione interattiva](assets/ic_web_hyperlink_new.png)

1. Toccate **Paga ora** nell’area di destinazione e toccate **+** per aggiungere un componente **Immagine** .
1. Toccate il componente Immagine e selezionate ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà dell’immagine vengono visualizzate nel riquadro a sinistra:

   1. Specificate **PayNow** come nome dell&#39;immagine nel campo **Nome** .

   1. Toccate **Carica**, selezionate l&#39;immagine **PayNowWeb** salvata nel file system locale, quindi toccate **Apri**.

   1. Toccate ![done_icon](assets/done_icon.png) per salvare le proprietà dell&#39;immagine.

1. In base al caso di utilizzo, inserire un pulsante **Iscrizione** nella comunicazione interattiva che offra all&#39;utente la possibilità di iscriversi ai servizi a valore aggiunto facendo clic sul pulsante.

   Ripetere i passaggi da 13 a 17 per aggiungere un pulsante **Iscrizione** all&#39;area di destinazione Servizi **aggiunti** valori e aggiungere l&#39;immagine **ValueAddedServicesWeb** .

## Creazione di comunicazioni interattive per la stampa e il Web con sincronizzazione automatica {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

È inoltre possibile creare una comunicazione interattiva abilitando la sincronizzazione automatica tra i canali Stampa e Web. Per attivare la sincronizzazione automatica, selezionate l’opzione Stampa come principale durante la creazione della comunicazione interattiva. Selezionando l&#39;opzione Stampa come principale, il contenuto, l&#39;ereditarietà e il binding dei dati del canale Web vengono derivati dal canale Stampa. Inoltre, garantisce che le modifiche apportate al canale Stampa si riflettano sul canale Web.

Per derivare il contenuto del canale Web utilizzando il canale di stampa, eseguire la procedura seguente:

1. Accedete all’istanza di creazione di AEM e andate a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Toccate **Crea** e selezionate Comunicazione **** interattiva. Viene visualizzata la procedura guidata **Crea comunicazione** interattiva.
1. Specificate **create_first_ic** nel campo **Titolo** e **Nome** . Selezionare **FDM_Create_First_IC** come modello dati modulo e toccare **Avanti**.
1. Nella procedura guidata **Canali** :

   1. Specificate **create_first_ic_print_template** come modello di stampa e toccate **Seleziona**.

   1. Selezionate la casella di controllo **Usa stampa come principale per canale** Web.
   1. Specificate la cartella **Create_First_IC_templates** > **Create_First_IC_Web_Template** come modello Web e toccate **Seleziona**.

   1. Toccate **Crea**.

   Viene visualizzato un messaggio di conferma della corretta creazione della comunicazione interattiva.

1. Toccate **Modifica** per aprire la comunicazione interattiva nel riquadro a destra.
1. Esegui i passaggi 6 - 15 della sezione [Crea comunicazione interattiva per canale](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel) di stampa.
1. Toccate la scheda **Canali** dal riquadro a sinistra e toccate **Web** per generare automaticamente il contenuto per il canale Web dal canale Stampa.
1. Poiché la casella **Usa stampa come master per canale** Web è selezionata al punto 4, il contenuto e i binding vengono generati automaticamente per il canale Web dal canale Stampa.

   Il contenuto del canale di stampa viene inserito sotto il contenuto del modello del canale Web. Per modificare il contenuto del canale Web generato automaticamente dal canale Stampa, è possibile annullare l&#39;ereditarietà per qualsiasi area di destinazione.

   Passa il cursore del mouse sull’area di destinazione desiderata nel canale Web e seleziona ![Annulla ereditarietà](assets/cancelinheritance.png) (Annulla ereditarietà), quindi tocca **Sì** nella finestra di dialogo **Annulla ereditarietà**.

   ![Annulla ereditarietà](assets/cancel_inheritance_web_channel_new.png)

   Se è stata annullata l’ereditarietà di un componente, è possibile riattivarlo. Per abilitare nuovamente l&#39;ereditarietà, passate il puntatore del mouse sul contorno dell&#39;area di destinazione interessata, che include il componente, e toccate ![renableinheritance](assets/reenableinheritance.png).

1. Selezionate la scheda **Contenuto** nel riquadro a sinistra.
1. Trascinate il contenuto del canale Web generato automaticamente nei pannelli esistenti nel modello Web utilizzando la struttura del contenuto. Di seguito è riportato l’elenco dei componenti che devono essere ridisposti:

   * Componente Dettagli fatturazione - Pannello Dettagli fatturazione
   * Componente Dettagli cliente - Pannello Dettagli cliente
   * Riepilogo distinta, componente, al pannello Riepilogo fatturazione
   * Riepilogo del componente Addebiti nel pannello Riepilogo spese
   * Frammento di layout (tabella) nel pannello Chiamate dettagliate

   ![Struttura contenuto Web](assets/ic_web_content_tree_new.png)

1. Ripetete i passaggi da 13 a 18 di [Create Interactive Communication for Web channel](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) per inserire i collegamenti ipertestuali **Pay Now** e **Subscribe** nel canale Web della Comunicazione interattiva.

