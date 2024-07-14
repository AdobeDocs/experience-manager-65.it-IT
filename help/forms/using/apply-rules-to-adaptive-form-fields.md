---
title: Applicare le regole ai campi del modulo adattivo
description: Crea regole per aggiungere interattività, logica di business e convalide intelligenti a un modulo adattivo.
page-status-flag: de-activated
products: SG_EXPERIENCEMANAGER/6.3/FORMS
exl-id: 0202ca65-21ef-4477-b704-7b52314a7d7b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 0%

---

# Tutorial: applicare regole ai campi del modulo adattivo {#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

Questo tutorial è un passaggio della serie [Creare il primo modulo adattivo](/help/forms/using/create-your-first-adaptive-form.md). L’Adobe consiglia di seguire la serie in sequenza cronologica per comprendere, eseguire e dimostrare il caso di utilizzo completo dell’esercitazione.

## Informazioni sull’esercitazione {#about-the-tutorial}

È possibile utilizzare le regole per aggiungere interattività, logica di business e convalide intelligenti a un modulo adattivo. I moduli adattivi hanno un editor di regole integrato. L’editor di regole fornisce una funzionalità di trascinamento della selezione, simile alle visite guidate. Il metodo di trascinamento della selezione è il metodo più rapido e semplice per creare regole. L’editor di regole fornisce anche una finestra di codice per gli utenti interessati a testare le loro abilità di codifica o a portare le regole a un livello successivo.

Per ulteriori informazioni sull&#39;editor di regole, consulta [Editor di regole di Forms adattivo](/help/forms/using/rule-editor.md).

Entro la fine dell’esercitazione imparerai a creare regole per:

* Richiama un servizio Modello dati modulo per recuperare i dati dal database
* Richiama un servizio Modello dati modulo per aggiungere dati al database
* Eseguire un controllo delle convalide e visualizzare i messaggi di errore

Le immagini GIF interattive alla fine di ogni sezione dell&#39;esercitazione consentono di apprendere e convalidare al volo la funzionalità del modulo che si sta creando.

## Passaggio 1: recuperare un record cliente dal database {#retrieve-customer-record}

Hai creato un modello dati modulo seguendo l&#39;articolo [Crea modello dati modulo](/help/forms/using/create-form-data-model.md). Ora è possibile utilizzare l&#39;editor di regole per richiamare i servizi Forms Data Model per recuperare e aggiungere informazioni al database.

A ogni cliente viene assegnato un numero ID cliente univoco, che consente di identificare i dati rilevanti del cliente in un database. La procedura seguente utilizza l’ID cliente per recuperare informazioni dal database:

1. Apri il modulo adattivo per la modifica.

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. Seleziona il campo **[!UICONTROL ID cliente]** e l&#39;icona **[!UICONTROL Modifica regole]**. Viene visualizzata la finestra Editor regole.
1. Seleziona l&#39;icona **[!UICONTROL + Crea]** per aggiungere una regola. Viene aperto l&#39;Editor visivo.

   Nell&#39;editor visivo, l&#39;istruzione **[!UICONTROL WHEN]** è selezionata per impostazione predefinita. Inoltre, l&#39;oggetto modulo (in questo caso, **[!UICONTROL ID cliente]**) da cui hai avviato l&#39;editor di regole è specificato nell&#39;istruzione **[!UICONTROL WHEN]**.

1. Seleziona l&#39;elenco a discesa **[!UICONTROL Seleziona stato]** e seleziona **[!UICONTROL è cambiato]**.

   ![quando customeridischanged](assets/whencustomeridischanged.png)

1. Nell&#39;istruzione **[!UICONTROL THEN]**, selezionare **[!UICONTROL Richiama servizio]** dal menu a discesa **[!UICONTROL Seleziona azione]**.
1. Selezionare il servizio **[!UICONTROL Recupera indirizzo di spedizione]** dal menu a discesa **[!UICONTROL Seleziona]**.
1. Trascina il campo **[!UICONTROL ID cliente]** dalla scheda Oggetti modulo all&#39;oggetto **[!UICONTROL Rilascia o seleziona qui]** nella casella **[!UICONTROL INPUT]**.

   ![dropobjectstoinputfield-recuperedata](assets/dropobjectstoinputfield-retrievedata.png)

1. Trascinare il campo **[!UICONTROL ID cliente, nome, indirizzo di spedizione, stato e CAP]** dalla scheda Oggetti modulo al campo **[!UICONTROL Rilascia oggetto o seleziona qui]** nella casella **[!UICONTROL OUTPUT]**.

   ![dropobjectstooutputfield-recuperedata](assets/dropobjectstooutputfield-retrievedata.png)

   Seleziona **[!UICONTROL Fine]** per salvare la regola. Nella finestra dell&#39;editor di regole, seleziona **[!UICONTROL Chiudi]**.

1. Visualizza l’anteprima del modulo adattivo. Immetti un ID nel campo **[!UICONTROL ID cliente]**. Il modulo ora può recuperare i dettagli del cliente dal database.

   ![informazioni-recupero](assets/retrieve-information.gif)

## Passaggio 2: aggiungere l&#39;indirizzo del cliente aggiornato al database {#updated-customer-address}

Dopo aver recuperato i dettagli del cliente dal database, puoi aggiornare l’indirizzo di spedizione, lo stato e il codice postale. La procedura seguente richiama un servizio del modello dati modulo per aggiornare le informazioni sul cliente nel database:

1. Seleziona il campo **[!UICONTROL Invia]** e l&#39;icona **[!UICONTROL Modifica regole]**. Viene visualizzata la finestra Editor regole.
1. Seleziona la regola **[!UICONTROL Invia - Fai clic su]** e seleziona l&#39;icona **[!UICONTROL Modifica]**. Vengono visualizzate le opzioni per modificare la regola di invio.

   ![submit-rule](assets/submit-rule.png)

   Nell&#39;opzione WHEN sono già selezionate le opzioni **[!UICONTROL Invia]** e **[!UICONTROL selezionate]**.

   ![invia-è-cliccato](assets/submit-is-clicked.png)

1. Nell&#39;opzione **[!UICONTROL THEN]**, selezionare l&#39;opzione **[!UICONTROL + Aggiungi istruzione]**. Selezionare **[!UICONTROL Richiama servizio]** dal menu a discesa **[!UICONTROL Seleziona azione]**.
1. Selezionare il servizio **[!UICONTROL Aggiorna indirizzo di spedizione]** dal menu a discesa **[!UICONTROL Seleziona]**.

   ![indirizzo-spedizione-aggiornamento](assets/update-shipping-address.png)

   ![dropobjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. Trascinare e rilasciare il campo **[!UICONTROL Indirizzo di spedizione, Stato e CAP]** dalla scheda [!UICONTROL Oggetti modulo] alla proprietà .nome tabella corrispondente (ad esempio, customerdetails.shippingAddress) dell&#39;oggetto **[!UICONTROL Rilasciare o selezionare qui]** nella casella **[!UICONTROL INPUT]**. Tutti i campi con prefisso tablename (ad esempio, customerdetails in this use case) fungono da dati di input per il servizio di aggiornamento. Tutto il contenuto fornito in questi campi viene aggiornato nell’origine dati.

   >[!NOTE]
   >
   >Non trascinare i campi **[!UICONTROL Nome]** e **[!UICONTROL ID cliente]** nella proprietà tablename.property corrispondente, ad esempio customerdetails.name. Consente di evitare di aggiornare il nome e l’ID del cliente per errore.

1. Trascina il campo **[!UICONTROL ID cliente]** dalla scheda [!UICONTROL Oggetti modulo] al campo ID nella casella **[!UICONTROL INPUT]**. I campi senza un nome di tabella preceduto (ad esempio, customerdetails in questo caso d’uso) fungono da parametro di ricerca per il servizio di aggiornamento. Il campo **[!UICONTROL id]** in questo caso d&#39;uso identifica in modo univoco un record nella tabella **customerdetails**.
1. Seleziona **[!UICONTROL Fine]** per salvare la regola. Nella finestra dell&#39;editor di regole, seleziona **[!UICONTROL Chiudi]**.
1. Visualizza l’anteprima del modulo adattivo. Recupera i dettagli di un cliente, aggiorna l’indirizzo di spedizione e invia il modulo. Quando recuperi nuovamente i dettagli dello stesso cliente, viene visualizzato l’indirizzo di spedizione aggiornato.

## Passaggio 3: (sezione Bonus) Utilizza l’editor di codice per eseguire convalide e visualizzare messaggi di errore {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

Eseguire la convalida del modulo per verificare che i dati immessi nel modulo siano corretti e che venga visualizzato un messaggio di errore in caso di dati errati. Ad esempio, se nel modulo viene inserito un ID cliente non esistente, deve essere visualizzato un messaggio di errore.

I moduli adattivi forniscono diversi componenti con convalide incorporate, ad esempio e-mail e campi numerici che puoi utilizzare per casi d’uso comuni. Utilizza l’editor di regole per i casi d’uso avanzati, ad esempio, per visualizzare un messaggio di errore quando il database restituisce record zero (0) (nessun record).

Nella procedura seguente viene illustrato come creare una regola per visualizzare un messaggio di errore se l&#39;ID cliente immesso nel modulo non esiste nel database. La regola porta inoltre lo stato attivo al campo **[!UICONTROL ID cliente]** e lo reimposta. La regola utilizza [l&#39;API dataIntegrationUtils del servizio modello dati modulo](/help/forms/using/invoke-form-data-model-services.md) per verificare se l&#39;ID cliente esiste nel database.

1. Selezionare il campo **[!UICONTROL ID cliente]** e l&#39;icona `Edit Rules`. Viene visualizzata la finestra [!UICONTROL Editor regole].
1. Seleziona l&#39;icona **[!UICONTROL + Crea]** per aggiungere una regola. Viene aperto l&#39;Editor visivo.

   Nell&#39;editor visivo, l&#39;istruzione **[!UICONTROL WHEN]** è selezionata per impostazione predefinita. Inoltre, l&#39;oggetto modulo (in questo caso, **[!UICONTROL ID cliente]**) da cui hai avviato l&#39;editor di regole è specificato nell&#39;istruzione **[!UICONTROL WHEN]**.

1. Seleziona l&#39;elenco a discesa **[!UICONTROL Seleziona stato]** e seleziona **[!UICONTROL è cambiato]**.

   ![quando customeridischanged](assets/whencustomeridischanged.png)

   Nell&#39;istruzione **[!UICONTROL THEN]**, selezionare **[!UICONTROL Richiama servizio]** dal menu a discesa **[!UICONTROL Seleziona azione]**.

1. Passare da **[!UICONTROL Editor visivo]** a **[!UICONTROL Editor di codice]**. Il comando dell&#39;interruttore si trova sul lato destro della finestra. Viene visualizzato l&#39;Editor di codice, con un codice simile al seguente:

   ![editor di codice](assets/code-editor.png)

1. Sostituisci la sezione della variabile di input con il seguente codice:

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. Sostituisci la sezione `guidelib.dataIntegrationUtils.executeOperation (operationInfo, inputs, outputs)` con il seguente codice:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, function (result) {
     if (result) {
         result = JSON.parse(result);
       customer_Name.value = result.name;
       customer_Shipping_Address = result.shippingAddress;
     } else {
       if(window.confirm("Invalid Customer ID. Provide a valid customer ID")) {
             customer_Name.value = " ";
            guideBridge.setFocus(customer_ID);
       }
     }
   });
   ```

1. Visualizza l’anteprima del modulo adattivo. Immetti un ID cliente errato. Viene visualizzato un messaggio di errore.

   ![display-validation-error](assets/display-validation-error.gif)
