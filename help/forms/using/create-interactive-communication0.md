---
title: "Tutorial: creare la comunicazione interattiva"
seo-title: Create an Interactive Communication for Print and Web
description: Creare una comunicazione interattiva utilizzando tutti gli elementi di base
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

# Tutorial: creare una comunicazione interattiva {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

Questo tutorial è un passaggio del [Creare la prima comunicazione interattiva](/help/forms/using/create-your-first-interactive-communication.md) serie. Si consiglia di seguire la serie in sequenza cronologica per comprendere, eseguire e dimostrare il caso di utilizzo completo dell’esercitazione.

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

1. Accedi all’istanza di authoring dell’AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Tocca **Crea** e seleziona **Comunicazione interattiva**. Il **Creare una comunicazione interattiva** viene visualizzata la procedura guidata.
1. Specifica **create_first_ic** nel **Titolo** e **Nome** campo. Seleziona **FDM_Create_First_IC** come modello dati del modulo e tocca **Successivo**.
1. In **Canali** procedura guidata:

   1. Specifica **create_first_ic_print_template** come modello di stampa e tocca **Seleziona**. Assicurati che **Usa stampa come master per canale web** non è selezionata.

   1. Specifica **Create_First_IC_templates** cartella > **Crea_Primo_IC_Modello_Web** come modello Web e tocca **Seleziona**.

   1. Tocca **Crea**.

   Viene visualizzato un messaggio di conferma che la comunicazione interattiva è stata creata correttamente.

1. Tocca **Modifica** per aprire la comunicazione interattiva nel riquadro di destra.
1. Vai a **Risorse** e applica il filtro per visualizzare solo i frammenti di documento nel riquadro a sinistra.
1. Trascina i seguenti frammenti di documento nelle aree di destinazione nella comunicazione interattiva:

   | Frammento di documento | Area di destinazione |
   |---|---|
   | bill_details_first_ic | Dettagli fattura |
   | customer_details_first_ic | DettagliCliente |
   | bill_summary_first_ic | Riepilogo fatture |
   | summary_charge_first_interactive_communication | Spese |

   ![Frammenti di documenti per comunicazioni interattive](assets/create_first_ic_doc_fragments_new.png)

1. Tocca **Grafici** area di destinazione, quindi tocca **+** per aggiungere un **Grafico** componente.
1. Tocca il componente Grafico e seleziona ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà del grafico vengono visualizzate nel riquadro a sinistra:

   1. Specificare un nome per il grafico.
   1. Seleziona **Torta** dal **Tipo di grafico** elenco a discesa.
   1. Seleziona la **calltype** proprietà dal **chiamate** tipo di oggetto modello dati in **Asse X** sezione. Tocca ![done_icon](assets/done_icon.png).
   1. Seleziona **Frequenza** dal **Funzione** elenco a discesa.
   1. Seleziona la **calltype** proprietà dal **chiamate** tipo di oggetto modello dati in **Asse Y** sezione. Tocca ![done_icon](assets/done_icon.png).
   1. Tocca ![done_icon](assets/done_icon.png) per salvare le proprietà del grafico.

1. Vai a **Risorse** e applica il filtro per visualizzare solo i frammenti di layout nel riquadro a sinistra. Trascina la selezione **table_lf** frammento di layout al **Chiamate dettagliate** area di destinazione.
1. Selezionare il campo di testo nella **Data** colonna e tocco ![configure_icon](assets/configure_icon.png) (Configura).
1. Seleziona **Oggetto modello dati** dal **Tipo di associazione** e selezionare **chiamate** > **calldate**. Tocca ![done_icon](assets/done_icon.png) due volte per salvare le proprietà.

   Analogamente, crea associazione con **calltime**, **callnumber**, **callduration**, e **callcharge** per i campi di testo nella **Ora**, **Numero**, **Durata**, e **Spese** colonne.

1. Tocca **PayNow** area di destinazione, quindi tocca **+** per aggiungere un **Immagine** componente.
1. Tocca il componente Immagine e seleziona ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà dell’immagine vengono visualizzate nel riquadro a sinistra:

   1. Specifica **PayNow** come nome dell’immagine nella **Nome** campo.
   1. Tocca **Carica**, seleziona l’immagine salvata nel file system locale e tocca **Apri**.
   1. Tocca ![done_icon](assets/done_icon.png) per salvare le proprietà dell&#39;immagine.

1. Ripeti i passaggi 13 e 14 per aggiungere **ValueAddedServices** immagine al **ValueAddedServices** area di destinazione.

### Creare una comunicazione interattiva per il canale web {#create-interactive-communication-for-web-channel}

Di seguito è riportato l’elenco delle risorse già create in questa esercitazione e necessarie durante la creazione della comunicazione interattiva per il canale web:

**Modello Web:** [Crea_Primo_IC_Modello_Web](../../forms/using/create-templates-print-web.md)

**Modello dati modulo:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Frammenti di documenti:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charge_first_ic](../../forms/using/create-document-fragments.md)

**Immagini:** PayNowWeb e ValueAddedServicesWeb

1. Accedi all’istanza di authoring dell’AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Tocca **Crea** e seleziona **Comunicazione interattiva**. Il **Creare una comunicazione interattiva** viene visualizzata la procedura guidata.
1. Specifica **create_first_ic** nel **Titolo** e **Nome** campo. Seleziona **FDM_Create_First_IC** come modello dati del modulo e tocca **Successivo**.
1. In **Canali** procedura guidata:

   1. Specifica **create_first_ic_print_template** come modello di stampa e tocca **Seleziona**. Assicurati che **Usa stampa come master per canale web** non è selezionata.

   1. Specifica **Create_First_IC_templates** cartella > **Crea_Primo_IC_Modello_Web** come modello Web e tocca **Seleziona**.

   1. Tocca **Crea**.

   Viene visualizzato un messaggio di conferma che la comunicazione interattiva è stata creata correttamente.

1. Tocca **Modifica** per aprire la comunicazione interattiva nel riquadro di destra.
1. Tocca il **Canali** dal riquadro a sinistra e tocca **Web**.
1. Vai a **Risorse** e applica il filtro per visualizzare solo i frammenti di documento nel riquadro a sinistra.
1. Trascina i seguenti frammenti di documento nelle aree di destinazione nella comunicazione interattiva:

   | Frammento di documento | Area di destinazione |
   |---|---|
   | bill_details_first_ic | Dettagli fattura |
   | customer_details_first_ic | DettagliCliente |
   | bill_summary_first_ic | Riepilogo fatture |
   | summary_charge_first_interactive_communication | Spese |

1. Tocca **Riepilogo addebiti** area di destinazione, quindi tocca **+** per aggiungere un **Grafico** componente.
1. Tocca il componente Grafico e seleziona ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà del grafico vengono visualizzate nel riquadro a sinistra:

   1. Specificare un nome per il grafico.
   1. Seleziona **Torta** dal **Tipo di grafico** elenco a discesa.

   1. Seleziona la **calltype** proprietà dal **chiamate** tipo di oggetto modello dati in **Asse X** sezione. Tocca ![done_icon](assets/done_icon.png).

   1. Seleziona **Frequenza** dal **Funzione** elenco a discesa.

   1. Seleziona la **calltype** proprietà dal **chiamate** tipo di oggetto modello dati in **Asse Y** sezione. Tocca ![done_icon](assets/done_icon.png).

   1. Tocca ![done_icon](assets/done_icon.png) per salvare le proprietà del grafico.

1. Seleziona la **Origini dati** dal riquadro di sinistra e trascinare e rilasciare la **chiamate** oggetto modello dati al **Chiamate dettagliate** area di destinazione. Tutte le proprietà in **chiamate** l’oggetto modello dati viene visualizzato come colonne di tabella nel **Chiamate dettagliate** area di destinazione nel riquadro di destra.

   In base al caso d’uso, nella tabella sono necessarie le colonne Data chiamata, Ora chiamata, Numero chiamata, Durata chiamata e Spese di chiamata.

   ![Tabella per la comunicazione interattiva](assets/table_ic_web_new.png)

1. Seleziona **Mobilità** intestazione di colonna della tabella e selezione **Altre opzioni** > **Elimina colonna**. Analogamente, elimina il **Tipo di chiamata** colonna.
1. Seleziona la **Calldate** intestazione di colonna della tabella e tocco ![modifica](assets/edit.png) (Modifica) per rinominare il testo in **Data chiamata**. Analogamente, rinominare altre intestazioni di colonna nella tabella.
1. In base al caso d’uso, inserisci un **Paga ora** nella comunicazione interattiva che fornisce all’utente un’opzione per effettuare il pagamento facendo clic sul pulsante. Per inserire il pulsante, effettua le seguenti operazioni:

   1. Tocca **Paga ora** area di destinazione, quindi tocca **+** per aggiungere un **Testo** componente.

   1. Tocca il componente testo e tocca ![modifica](assets/edit.png) (Modifica).
   1. Rinomina il testo in **Paga ora**.
   1. Seleziona il testo e tocca l’icona Collegamento ipertestuale.
   1. Specifica l&#39;URL del pagamento in **Percorso** campo.
   1. Seleziona **Nuova scheda** da **Target** elenco a discesa.

   1. Tocca ![done_icon](assets/done_icon.png) per salvare le proprietà del collegamento ipertestuale.

1. Seleziona **Stile** dall’elenco a discesa accanto al **Anteprima** opzione.

   ![Seleziona la modalità Stile per la comunicazione interattiva](assets/select_style_ic_web_new.png)

1. Personalizzare lo stile del testo del collegamento ipertestuale per visualizzarlo come pulsante nella comunicazione interattiva attenendosi alla procedura seguente:

   1. Tocca il componente testo e seleziona ![modifica](assets/edit.png) (Modifica).
   1. In **Bordo** , specificare **1,5 px** as **Larghezza bordo**, seleziona **Solido** as **Stile bordo**, e specificare **46 px** as **Raggio bordo**.

   1. Selezionare Rosso come colore di sfondo per il pulsante dal menu **Sfondo** sezione.
   1. In **Margine** campo per **Dimension e posizione** , toccare la sezione **Modifica simultaneamente** e impostare **Destra** margine come **450 px**. I campi Superiore, Inferiore e Sinistro vengono impostati come vuoti.

   ![Inserisci collegamento ipertestuale nella comunicazione interattiva](assets/ic_web_hyperlink_new.png)

1. Tocca **Paga ora** area di destinazione, quindi tocca **+** per aggiungere un **Immagine** componente.
1. Tocca il componente Immagine e seleziona ![configure_icon](assets/configure_icon.png) (Configura). Le proprietà dell’immagine vengono visualizzate nel riquadro a sinistra:

   1. Specifica **PayNow** come nome dell’immagine nella **Nome** campo.

   1. Tocca **Carica**, seleziona la **PayNowWeb** immagine salvata nel file system locale e tocca **Apri**.

   1. Tocca ![done_icon](assets/done_icon.png) per salvare le proprietà dell&#39;immagine.

1. In base al caso d’uso, inserisci un **Abbonati** nella comunicazione interattiva che fornisce all’utente un’opzione per abbonarsi ai servizi a valore aggiunto facendo clic sul pulsante.

   Ripetere i passaggi da 13 a 17 per aggiungere un **Abbonati** pulsante per **Servizi a valore aggiunto** area di destinazione e aggiungere **ValueAddedServicesWeb** immagine.

## Creazione di comunicazioni interattive per la stampa e il Web con sincronizzazione automatica {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

È inoltre possibile creare una comunicazione interattiva abilitando la sincronizzazione automatica tra i canali di stampa e web. Per abilitare la sincronizzazione automatica, seleziona l’opzione Stampa come principale durante la creazione della comunicazione interattiva. Selezionando l’opzione Stampa come principale, il contenuto, l’ereditarietà e l’associazione dati del canale web vengono derivati dal canale di stampa. Inoltre, assicura che le modifiche apportate nel canale di stampa vengano applicate al canale web.

Esegui la procedura seguente per derivare il contenuto del canale web utilizzando il canale di stampa:

1. Accedi all’istanza di authoring dell’AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Tocca **Crea** e seleziona **Comunicazione interattiva**. Il **Creare una comunicazione interattiva** viene visualizzata la procedura guidata.
1. Specifica **create_first_ic** nel **Titolo** e **Nome** campo. Seleziona **FDM_Create_First_IC** come modello dati del modulo e tocca **Successivo**.
1. In **Canali** procedura guidata:

   1. Specifica **create_first_ic_print_template** come modello di stampa e tocca **Seleziona**.

   1. Seleziona la **Usa stampa come master per canale web** casella di controllo.
   1. Specifica **Create_First_IC_templates** cartella > **Crea_Primo_IC_Modello_Web** come modello Web e tocca **Seleziona**.

   1. Tocca **Crea**.

   Viene visualizzato un messaggio di conferma che la comunicazione interattiva è stata creata correttamente.

1. Tocca **Modifica** per aprire la comunicazione interattiva nel riquadro di destra.
1. Esegui i passaggi 6-15 di [Crea comunicazione interattiva per canale di stampa](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel) sezione.
1. Tocca il **Canali** dal riquadro a sinistra e tocca **Web** per generare automaticamente contenuti per il canale web dal canale di stampa.
1. Come **Usa stampa come master per canale web** Se la casella di controllo è selezionata nel passaggio 4, il contenuto e le associazioni vengono generati automaticamente per il canale web dal canale di stampa.

   Il contenuto del canale di stampa viene inserito sotto il contenuto del modello del canale web. Per modificare il contenuto del canale web generato automaticamente dal canale di stampa, puoi annullare l’ereditarietà per qualsiasi area di destinazione.

   Passa il puntatore del mouse sull’area di destinazione pertinente nel canale web e seleziona ![cancella ereditarietà](assets/cancelinheritance.png) (Annulla ereditarietà) e quindi in **Annulla ereditarietà** finestra di dialogo, tocca **Sì**.

   ![Annulla ereditarietà](assets/cancel_inheritance_web_channel_new.png)

   Se hai annullato l’ereditarietà di un componente, puoi riabilitarlo. Per riabilitare l’ereditarietà, passa il cursore sul limite dell’area di destinazione pertinente, che include il componente, e tocca ![riabilita ereditarietà](assets/reenableinheritance.png).

1. Seleziona la **Contenuto** nel riquadro a sinistra.
1. Trascinare il contenuto del canale Web generato automaticamente sui pannelli esistenti nel modello Web utilizzando la struttura del contenuto. Di seguito è riportato l’elenco dei componenti che devono essere ridisposti:

   * Dettagli distinta componente nel pannello Dettagli distinta
   * Componente Dettagli cliente nel pannello Dettagli cliente
   * Pannello Sintetico distinta - Sintetico distinta
   * Componente Riepilogo addebiti nel pannello Riepilogo addebiti
   * Frammento layout (tabella) nel pannello Chiamate dettagliate

   ![Struttura contenuto Web](assets/ic_web_content_tree_new.png)

1. Ripeti i passaggi da 13 a 18 di [Creare una comunicazione interattiva per il canale web](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) per inserire **Paga ora** e **Abbonati** collegamenti ipertestuali nel canale web della comunicazione interattiva.
