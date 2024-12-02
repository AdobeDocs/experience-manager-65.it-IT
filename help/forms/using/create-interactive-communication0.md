---
title: 'Tutorial: creare una comunicazione interattiva '
description: Creare una comunicazione interattiva utilizzando tutti gli elementi di base
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: aaacee66-6bbe-498b-91b1-3a9545ff1aeb
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 0%

---

# Tutorial: creare una comunicazione interattiva {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

Questo tutorial è un passaggio della serie [Crea la tua prima comunicazione interattiva](/help/forms/using/create-your-first-interactive-communication.md). Si consiglia di seguire la serie in sequenza cronologica per comprendere, eseguire e dimostrare il caso di utilizzo completo dell’esercitazione.

Dopo aver creato tutti i blocchi predefiniti, ad esempio il modello di dati del modulo, i frammenti di documento, i modelli e i temi per la versione web, puoi iniziare a creare una comunicazione interattiva.

Le comunicazioni interattive possono essere distribuite attraverso due canali: stampa e web. Puoi anche creare una comunicazione interattiva con il canale di stampa come principale. L’opzione Stampa come master per il canale web assicura che il contenuto, l’ereditarietà e l’associazione dati del canale web siano derivati dal canale di stampa. Inoltre, assicura che le modifiche apportate nel canale di stampa siano sincronizzate nel canale web. Tuttavia, gli autori delle comunicazioni interattive possono interrompere l’ereditarietà di componenti specifici nel canale web.

Questo tutorial illustra i passaggi necessari per creare comunicazioni interattive per i canali di stampa e web. Al termine di questa esercitazione, sarai in grado di:

* Creare una comunicazione interattiva per il canale di stampa
* Creare comunicazioni interattive per il canale web
* Creare comunicazioni interattive a mezzo Stampa e Web con Stampa come principale

## Creazione di comunicazioni interattive per la stampa e il Web senza sincronizzazione {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### Crea comunicazione interattiva per canale di stampa {#create-interactive-communication-for-print-channel}

Di seguito è riportato un elenco delle risorse già create in questa esercitazione e necessarie durante la creazione della comunicazione interattiva per il canale di stampa:

**Modello di stampa:** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**Modello dati modulo:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Frammenti di documenti:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charge_first_ic](../../forms/using/create-document-fragments.md)

**Frammenti layout:** [table_lf](../../forms/using/create-templates-print-web.md)

**Immagini:** PayNow e ValueAddedServices

1. Accedi all&#39;istanza di creazione dell&#39;AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona **Crea** e seleziona **Comunicazione interattiva**. Viene visualizzata la procedura guidata **Crea comunicazione interattiva**.
1. Specifica **create_first_ic** nel campo **Title** e nel campo **Name**. Seleziona **FDM_Create_First_IC** come modello dati del modulo e seleziona **Next**.
1. Nella procedura guidata **Canali**:

   1. Specifica **create_first_ic_print_template** come modello di stampa e seleziona **Seleziona**. Verificare che la casella di controllo **Usa stampa come master per canale Web** non sia selezionata.

   1. Specifica la cartella **Create_First_IC_templates** > **Create_First_IC_Web_Template** come modello Web e seleziona **Seleziona**.

   1. Seleziona **Crea**.

   Viene visualizzato un messaggio di conferma che la comunicazione interattiva è stata creata correttamente.

1. Seleziona **Modifica** per aprire la comunicazione interattiva nel riquadro a destra.
1. Passa alla scheda **Assets** e applica il filtro per visualizzare solo i frammenti di documento nel riquadro a sinistra.
1. Trascina i seguenti frammenti di documento nelle aree di destinazione nella comunicazione interattiva:

   | Frammento di documento | Area di destinazione |
   |---|---|
   | bill_details_first_ic | Dettagli fattura |
   | customer_details_first_ic | DettagliCliente |
   | bill_summary_first_ic | Riepilogo fatture |
   | summary_charge_first_interactive_communication | Spese |

   ![Frammenti di documenti per comunicazioni interattive](assets/create_first_ic_doc_fragments_new.png)

1. Selezionare l&#39;area di destinazione **Grafici** e selezionare **+** per aggiungere un componente **Grafico**.
1. Selezionare il componente Grafico e selezionare ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà del grafico vengono visualizzate nel riquadro a sinistra:

   1. Specificare un nome per il grafico.
   1. Selezionare **Torta** dall&#39;elenco a discesa **Tipo di grafico**.
   1. Selezionare la proprietà **calltype** dal tipo di oggetto del modello dati **calls** nella sezione **X-axis**. Seleziona ![icona_completato](assets/done_icon.png).
   1. Selezionare **Frequenza** dall&#39;elenco a discesa **Funzione**.
   1. Selezionare la proprietà **calltype** dal tipo di oggetto del modello dati **calls** nella sezione **Y-axis**. Seleziona ![icona_completato](assets/done_icon.png).
   1. Seleziona ![icona_fine](assets/done_icon.png) per salvare le proprietà del grafico.

1. Vai alla scheda **Assets** e applica il filtro per visualizzare solo i frammenti di layout nel riquadro a sinistra. Trascina il frammento di layout **table_lf** nell&#39;area di destinazione **Chiamate dettagliate**.
1. Selezionare il campo di testo nella colonna **Data** e selezionare ![configure_icon](assets/configure_icon.png) (Configura).
1. Selezionare **Oggetto modello dati** dall&#39;elenco a discesa **Tipo di associazione** e selezionare **chiamate** > **calldate**. Seleziona ![done_icon](assets/done_icon.png) due volte per salvare le proprietà.

   Analogamente, creare l&#39;associazione con **calltime**, **callnumber**, **callduration** e **callcharge** per i campi di testo nelle colonne **Time**, **Number**, **Duration** e **Charges** rispettivamente.

1. Seleziona l&#39;area di destinazione **PayNow** e seleziona **+** per aggiungere un componente **Image**.
1. Seleziona il componente Immagine e seleziona ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà dell’immagine vengono visualizzate nel riquadro a sinistra:

   1. Specifica **PayNow** come nome dell&#39;immagine nel campo **Name**.
   1. Selezionare **Carica**, selezionare l&#39;immagine salvata nel file system locale, quindi selezionare **Apri**.
   1. Seleziona ![icona_completato](assets/done_icon.png) per salvare le proprietà dell&#39;immagine.

1. Ripetere i passaggi 13 e 14 per aggiungere l&#39;immagine **ValueAddedServices** all&#39;area di destinazione **ValueAddedServices**.

### Creare una comunicazione interattiva per il canale web {#create-interactive-communication-for-web-channel}

Di seguito è riportato l’elenco delle risorse già create in questa esercitazione e necessarie durante la creazione della comunicazione interattiva per il canale web:

**Modello Web:** [Crea_Primo_IC_Modello_Web](../../forms/using/create-templates-print-web.md)

**Modello dati modulo:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Frammenti di documenti:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charge_first_ic](../../forms/using/create-document-fragments.md)

**Immagini:** PayNowWeb e ValueAddedServicesWeb

1. Accedi all&#39;istanza di creazione dell&#39;AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona **Crea** e seleziona **Comunicazione interattiva**. Viene visualizzata la procedura guidata **Crea comunicazione interattiva**.
1. Specifica **create_first_ic** nel campo **Title** e nel campo **Name**. Seleziona **FDM_Create_First_IC** come modello dati del modulo e seleziona **Next**.
1. Nella procedura guidata **Canali**:

   1. Specifica **create_first_ic_print_template** come modello di stampa e seleziona **Seleziona**. Verificare che la casella di controllo **Usa stampa come master per canale Web** non sia selezionata.

   1. Specifica la cartella **Create_First_IC_templates** > **Create_First_IC_Web_Template** come modello Web e seleziona **Seleziona**.

   1. Seleziona **Crea**.

   Viene visualizzato un messaggio di conferma che la comunicazione interattiva è stata creata correttamente.

1. Seleziona **Modifica** per aprire la comunicazione interattiva nel riquadro a destra.
1. Selezionare la scheda **Canali** dal riquadro di sinistra e selezionare **Web**.
1. Passa alla scheda **Assets** e applica il filtro per visualizzare solo i frammenti di documento nel riquadro a sinistra.
1. Trascina i seguenti frammenti di documento nelle aree di destinazione nella comunicazione interattiva:

   | Frammento di documento | Area di destinazione |
   |---|---|
   | bill_details_first_ic | Dettagli fattura |
   | customer_details_first_ic | DettagliCliente |
   | bill_summary_first_ic | Riepilogo fatture |
   | summary_charge_first_interactive_communication | Spese |

1. Selezionare l&#39;area di destinazione **Riepilogo addebiti** e selezionare **+** per aggiungere un componente **Grafico**.
1. Selezionare il componente Grafico e selezionare ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà del grafico vengono visualizzate nel riquadro a sinistra:

   1. Specificare un nome per il grafico.
   1. Selezionare **Torta** dall&#39;elenco a discesa **Tipo di grafico**.

   1. Selezionare la proprietà **calltype** dal tipo di oggetto del modello dati **calls** nella sezione **X-axis**. Seleziona ![icona_completato](assets/done_icon.png).

   1. Selezionare **Frequenza** dall&#39;elenco a discesa **Funzione**.

   1. Selezionare la proprietà **calltype** dal tipo di oggetto del modello dati **calls** nella sezione **Y-axis**. Seleziona ![icona_completato](assets/done_icon.png).

   1. Seleziona ![icona_fine](assets/done_icon.png) per salvare le proprietà del grafico.

1. Seleziona la scheda **Origini dati** dal riquadro a sinistra e trascina l&#39;oggetto modello dati **chiamate** nell&#39;area di destinazione **Chiamate dettagliate**. Tutte le proprietà nell&#39;oggetto modello dati **calls** vengono visualizzate come colonne di tabella nell&#39;area di destinazione **Chiamate dettagliate** nel riquadro di destra.

   In base al caso d’uso, nella tabella sono necessarie le colonne Data chiamata, Ora chiamata, Numero chiamata, Durata chiamata e Spese di chiamata.

   ![Tabella per la comunicazione interattiva](assets/table_ic_web_new.png)

1. Selezionare **Mobilenum** intestazione colonna tabella e **Altre opzioni** > **Elimina colonna**. Eliminare la colonna **Calltype**.
1. Selezionare l&#39;intestazione di colonna della tabella **Calldate** e selezionare ![edit](assets/edit.png) (Modifica) per rinominare il testo in **Call Date**. Analogamente, rinominare altre intestazioni di colonna nella tabella.
1. In base al caso d&#39;uso, inserisci un pulsante **Paga ora** nella comunicazione interattiva che offre all&#39;utente l&#39;opzione di effettuare il pagamento facendo clic sul pulsante. Per inserire il pulsante, effettua le seguenti operazioni:

   1. Seleziona l&#39;area di destinazione **Paga ora** e seleziona **+** per aggiungere un componente **Testo**.

   1. Seleziona il componente testo e seleziona ![modifica](assets/edit.png) (Modifica).
   1. Rinomina il testo in **Paga ora**.
   1. Selezionare il testo e l&#39;icona Collegamento ipertestuale.
   1. Specifica l&#39;URL del pagamento nel campo **Percorso**.
   1. Seleziona **Nuova scheda** dall&#39;elenco a discesa **Target**.

   1. Seleziona ![done_icon](assets/done_icon.png) per salvare le proprietà del collegamento ipertestuale.

1. Seleziona **Stile** dall&#39;elenco a discesa accanto all&#39;opzione **Anteprima**.

   ![Seleziona modalità stile per comunicazione interattiva](assets/select_style_ic_web_new.png)

1. Personalizzare lo stile del testo del collegamento ipertestuale per visualizzarlo come pulsante nella comunicazione interattiva attenendosi alla procedura seguente:

   1. Seleziona il componente testo e seleziona ![modifica](assets/edit.png) (Modifica).
   1. Nella sezione **Bordo**, specifica **1.5px** come **Larghezza bordo**, seleziona **Solido** come **Stile bordo** e specifica **46px** come **Raggio bordo**.

   1. Seleziona Rosso come colore di sfondo per il pulsante dalla sezione **Sfondo**.
   1. Nel campo **Margine** per **Dimension e posizione**, seleziona l&#39;icona **Modifica contemporaneamente** e imposta il margine **Destra** come **450px**. I campi Superiore, Inferiore e Sinistro vengono impostati come vuoti.

   ![Inserisci collegamento ipertestuale nella comunicazione interattiva](assets/ic_web_hyperlink_new.png)

1. Seleziona l&#39;area di destinazione **Paga ora** e seleziona **+** per aggiungere un componente **Immagine**.
1. Seleziona il componente Immagine e seleziona ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà dell’immagine vengono visualizzate nel riquadro a sinistra:

   1. Specifica **PayNow** come nome dell&#39;immagine nel campo **Name**.

   1. Seleziona **Carica**, seleziona l&#39;immagine **PayNowWeb** salvata nel file system locale e seleziona **Apri**.

   1. Seleziona ![icona_completato](assets/done_icon.png) per salvare le proprietà dell&#39;immagine.

1. In base al caso d&#39;uso, inserisci un pulsante **Abbonati** nella comunicazione interattiva che offre all&#39;utente l&#39;opzione di abbonarsi ai servizi a valore aggiunto facendo clic sul pulsante.

   Ripetere i passaggi 13 - 17 per aggiungere un pulsante **Abbonati** all&#39;area di destinazione **Servizi aggiunti** e aggiungere l&#39;immagine **Servizi aggiunti**.

## Creazione di comunicazioni interattive per la stampa e il Web con sincronizzazione automatica {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

È inoltre possibile creare una comunicazione interattiva abilitando la sincronizzazione automatica tra i canali di stampa e web. Per abilitare la sincronizzazione automatica, seleziona l’opzione Stampa come principale durante la creazione della comunicazione interattiva. Selezionando l’opzione Stampa come principale, il contenuto, l’ereditarietà e l’associazione dati del canale web vengono derivati dal canale di stampa. Inoltre, assicura che le modifiche apportate nel canale di stampa vengano applicate al canale web.

Esegui la procedura seguente per derivare il contenuto del canale web utilizzando il canale di stampa:

1. Accedi all&#39;istanza di creazione dell&#39;AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona **Crea** e seleziona **Comunicazione interattiva**. Viene visualizzata la procedura guidata **Crea comunicazione interattiva**.
1. Specifica **create_first_ic** nel campo **Title** e nel campo **Name**. Seleziona **FDM_Create_First_IC** come modello dati del modulo e seleziona **Next**.
1. Nella procedura guidata **Canali**:

   1. Specifica **create_first_ic_print_template** come modello di stampa e seleziona **Seleziona**.

   1. Selezionare la casella di controllo **Usa stampa come master per canale Web**.
   1. Specifica la cartella **Create_First_IC_templates** > **Create_First_IC_Web_Template** come modello Web e seleziona **Seleziona**.

   1. Seleziona **Crea**.

   Viene visualizzato un messaggio di conferma che la comunicazione interattiva è stata creata correttamente.

1. Seleziona **Modifica** per aprire la comunicazione interattiva nel riquadro a destra.
1. Eseguire i passaggi da 6 a 15 della sezione [Crea comunicazione interattiva per il canale di stampa](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel).
1. Selezionare la scheda **Canali** dal riquadro di sinistra e selezionare **Web** per generare automaticamente il contenuto per il canale Web dal canale di stampa.
1. Poiché la casella di controllo **Usa stampa come master per canale Web** è selezionata nel passaggio 4, il contenuto e le associazioni vengono generati automaticamente per il canale Web dal canale di stampa.

   Il contenuto del canale di stampa viene inserito sotto il contenuto del modello del canale web. Per modificare il contenuto del canale web generato automaticamente dal canale di stampa, puoi annullare l’ereditarietà per qualsiasi area di destinazione.

   Passa il puntatore del mouse sull&#39;area di destinazione pertinente nel canale Web e seleziona ![cancella ereditarietà](assets/cancelinheritance.png) (Annulla ereditarietà), quindi nella finestra di dialogo **Annulla ereditarietà** seleziona **Sì**.

   ![Annulla ereditarietà](assets/cancel_inheritance_web_channel_new.png)

   Se hai annullato l’ereditarietà di un componente, puoi riabilitarlo. Per riabilitare l&#39;ereditarietà, passa il cursore del mouse sul limite dell&#39;area di destinazione pertinente, che include il componente, quindi seleziona ![reenableinheritance](assets/reenableinheritance.png).

1. Seleziona la scheda **Contenuto** nel riquadro a sinistra.
1. Trascinare il contenuto del canale Web generato automaticamente sui pannelli esistenti nel modello Web utilizzando la struttura del contenuto. Di seguito è riportato l’elenco dei componenti che devono essere ridisposti:

   * Dettagli distinta componente nel pannello Dettagli distinta
   * Componente Dettagli cliente nel pannello Dettagli cliente
   * Pannello Sintetico distinta - Sintetico distinta
   * Componente Riepilogo addebiti nel pannello Riepilogo addebiti
   * Frammento layout (tabella) nel pannello Chiamate dettagliate

   ![Struttura contenuto Web](assets/ic_web_content_tree_new.png)

1. Ripeti i passaggi 13 - 18 di [Crea comunicazione interattiva per il canale web](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) per inserire i collegamenti ipertestuali **Paga ora** e **Abbonati** nel canale web della comunicazione interattiva.
