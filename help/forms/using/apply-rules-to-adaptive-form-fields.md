---
title: '"NON PUBBLICARE L''Esercitazione: Applica regole ai campi modulo adattivi"'
seo-title: Applicazione di regole ai campi modulo adattivi
description: Creare regole per aggiungere interattività, business logic e convalide intelligenti a un modulo adattivo.
seo-description: Creare regole per aggiungere interattività, business logic e convalide intelligenti a un modulo adattivo.
page-status-flag: de-activated
uuid: 60f142aa-81ca-4333-8614-85a01e23e917
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 982eddba-2350-40e7-8a42-db02d28cf133
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---


# Esercitazione: Applicazione di regole ai campi modulo adattivi {#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

Questa esercitazione è un passaggio della serie [Crea il primo modulo](/help/forms/using/create-your-first-adaptive-form.md) adattivo. Adobe consiglia di seguire le serie in sequenza cronologica per comprendere, eseguire e dimostrare l’uso completo dell’esercitazione.

## Informazioni sull&#39;esercitazione {#about-the-tutorial}

È possibile utilizzare le regole per aggiungere interattività, logica aziendale e convalide intelligenti a un modulo adattivo. I moduli adattivi dispongono di un editor di regole integrato. L&#39;editor di regole fornisce una funzionalità di trascinamento, simile alle visite guidate. Il metodo di trascinamento della selezione è il metodo più veloce e semplice per creare le regole. L&#39;editor di regole fornisce inoltre una finestra di codice per gli utenti interessati a testare le proprie capacità di codifica o a portare le regole al livello successivo.

Per ulteriori informazioni sull&#39;editor di regole, vedere Editor di regole [per moduli adattivi](/help/forms/using/rule-editor.md).

Al termine dell&#39;esercitazione, verrà illustrato come creare delle regole per:

* Richiamo di un servizio Form Data Model per recuperare i dati dal database
* Richiamo di un servizio Form Data Model per aggiungere dati al database
* Eseguire un controllo delle convalide e visualizzare i messaggi di errore

Le immagini GIF interattive alla fine di ciascuna sezione dell&#39;esercitazione consentono di apprendere e convalidare al volo la funzionalità del modulo che si sta creando.

## Passaggio 1: Recuperare un record cliente dal database {#retrieve-customer-record}

È stato creato un modello dati modulo seguendo l&#39;articolo [Creazione del modello](/help/forms/using/create-form-data-model.md) dati del modulo. Ora è possibile utilizzare l&#39;editor di regole per richiamare i servizi Forms Data Model per recuperare e aggiungere informazioni al database.

A ogni cliente viene assegnato un numero ID cliente univoco, che consente di identificare i dati cliente rilevanti in un database. La procedura seguente utilizza l&#39;ID cliente per recuperare informazioni dal database:

1. Aprire il modulo adattivo per la modifica.

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. Toccate il campo ID **** cliente e toccate l&#39;icona **[!UICONTROL Modifica regole]** . Viene visualizzata la finestra Editor regole.
1. Toccate l&#39;icona **[!UICONTROL + Crea]** per aggiungere una regola. Viene aperto l&#39;editor visivo.

   Nell&#39;Editor visivo, l&#39;istruzione **[!UICONTROL WHEN]** è selezionata per impostazione predefinita. Inoltre, l&#39;oggetto modulo (in questo caso, ID **** cliente) dal quale è stato avviato l&#39;editor delle regole è specificato nell&#39;istruzione **[!UICONTROL WHEN]** .

1. Toccate il menu a discesa **[!UICONTROL Seleziona stato]** e selezionate **[!UICONTROL viene modificato]**.

   ![quando customeridischanged](assets/whencustomeridischanged.png)

1. Nell&#39;istruzione **[!UICONTROL THEN]** , selezionare **[!UICONTROL Richiama servizio]** dal menu a discesa **[!UICONTROL Seleziona azione]** .
1. Selezionare il servizio **[!UICONTROL Recupera indirizzo]** di spedizione dal menu a discesa **[!UICONTROL Seleziona]** .
1. Trascinare il campo ID **** cliente dalla scheda Oggetti modulo all&#39;oggetto **[!UICONTROL Drop oppure selezionare il campo qui]** nella casella **[!UICONTROL INPUT]** .

   ![dropobjectstoinputfield-retrieveedata](assets/dropobjectstoinputfield-retrievedata.png)

1. Trascinare il campo ID **[!UICONTROL cliente, Nome, Indirizzo di spedizione, Stato e CAP]** dalla scheda Oggetti modulo all&#39;oggetto **[!UICONTROL Drop oppure selezionare il campo qui]** nella casella **[!UICONTROL OUTPUT]** .

   ![dropobjectstooutputfield-retrieveedata](assets/dropobjectstooutputfield-retrievedata.png)

   Toccate **[!UICONTROL Fine]** per salvare la regola. Nella finestra dell&#39;editor delle regole, toccate **[!UICONTROL Chiudi]**.

1. Visualizzare l&#39;anteprima del modulo adattivo. Immettete un ID nel campo ID **** cliente. Il modulo ora può recuperare i dettagli dei clienti dal database.

   ![retrieve-information](assets/retrieve-information.gif)

## Passaggio 2: Aggiungere l&#39;indirizzo cliente aggiornato al database {#updated-customer-address}

Dopo aver recuperato i dettagli del cliente dal database, potete aggiornare l&#39;indirizzo di spedizione, lo stato e il codice postale. La procedura seguente richiama un servizio Form Data Model per aggiornare le informazioni dei clienti al database:

1. Selezionate il campo **[!UICONTROL Invia]** e toccate l&#39;icona **[!UICONTROL Modifica regole]** . Viene visualizzata la finestra Editor regole.
1. Selezionate la regola **[!UICONTROL Invia - Fate clic]** e toccate l&#39;icona **[!UICONTROL Modifica]** . Vengono visualizzate le opzioni per modificare la regola di invio.

   ![submit-rule](assets/submit-rule.png)

   Nell&#39;opzione WHEN, le opzioni **[!UICONTROL Invia]** e **[!UICONTROL selezionata]** sono già selezionate.

   ![submit-is-click](assets/submit-is-clicked.png)

1. Nell&#39;opzione **[!UICONTROL THEN]** , toccate l&#39;opzione **[!UICONTROL + Aggiungi istruzione]** . Selezionate **[!UICONTROL Richiama servizio]** dal menu a discesa **[!UICONTROL Seleziona azione]** .
1. Selezionare il servizio **[!UICONTROL Aggiorna indirizzo]** spedizione dal menu a discesa **[!UICONTROL Seleziona]** .

   ![update-shipping-address](assets/update-shipping-address.png)

1. ![dropobjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

   Trascinare il campo Indirizzo di **[!UICONTROL spedizione, Stato e CAP]** dalla scheda Oggetti modulo alla proprietà .nome tabella corrispondente (ad esempio, customdetails .ShippingAddress) dell&#39;oggetto **[!UICONTROL Drop oppure selezionare il campo qui]** nella casella **[!UICONTROL INPUT]** . Tutti i campi con il prefisso nome tabella (ad esempio, i dettagli del cliente in questo caso d’uso) fungono da dati di input per il servizio di aggiornamento. Tutto il contenuto fornito in questi campi viene aggiornato nell&#39;origine dati.

   >[!NOTE]
   >
   >Non trascinare i campi **[!UICONTROL Nome]** e ID **** cliente fino alla corrispondente tablespace.property (ad esempio, customdetails.name). Consente di evitare di aggiornare per errore nome e ID del cliente.

1. Trascinare il campo ID **** cliente dalla scheda Oggetti modulo al campo id nella casella **[!UICONTROL INPUT]** . I campi senza un nome di tabella prefisso (ad esempio, i dettagli del cliente in questo caso d’uso) fungono da parametro di ricerca per il servizio di aggiornamento. Il campo **[!UICONTROL id]** in questo caso d’uso identifica in modo univoco un record nella tabella dei dettagli del cliente.
1. Toccate **[!UICONTROL Fine]** per salvare la regola. Nella finestra dell&#39;editor delle regole, toccate **[!UICONTROL Chiudi]**.
1. Visualizzare l&#39;anteprima del modulo adattivo. Recuperare i dettagli di un cliente, aggiornare l&#39;indirizzo di spedizione e inviare il modulo. Quando recuperi nuovamente i dettagli dello stesso cliente, viene visualizzato l&#39;indirizzo di spedizione aggiornato.

## Passaggio 3: (sezione Bonus) Utilizzare l&#39;editor di codice per eseguire le convalide e visualizzare i messaggi di errore {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

È necessario eseguire la convalida sul modulo per verificare che i dati immessi nel modulo siano corretti e che venga visualizzato un messaggio di errore in caso di dati non corretti. Ad esempio, se nel modulo viene immesso un ID cliente non esistente, deve essere visualizzato un messaggio di errore.

I moduli adattivi forniscono diversi componenti con convalide integrate, ad esempio e-mail e campi numerici utilizzabili per casi di utilizzo comuni. Utilizzare l&#39;editor di regole per i casi di utilizzo avanzati, ad esempio, per visualizzare un messaggio di errore quando il database restituisce zero (0) record (nessun record).

La procedura seguente mostra come creare una regola per visualizzare un messaggio di errore se l&#39;ID cliente immesso nel modulo non esiste nel database. La regola attiva e ripristina il campo ID cliente. La regola utilizza [l&#39;API dataIntegrationUtils del servizio](/help/forms/using/invoke-form-data-model-services.md) del modello dati del modulo per verificare se l&#39;ID cliente esiste nel database.

1. Toccate il campo ID **** cliente e toccate l&#39; `Edit Rules` icona. Viene visualizzata la finestra Editor regole.
1. Toccate l&#39;icona **[!UICONTROL + Crea]** per aggiungere una regola. Viene aperto l&#39;editor visivo.

   Nell&#39;Editor visivo, l&#39;istruzione **[!UICONTROL WHEN]** è selezionata per impostazione predefinita. Inoltre, l&#39;oggetto modulo (in questo caso, ID **** cliente) dal quale è stato avviato l&#39;editor delle regole è specificato nell&#39;istruzione **[!UICONTROL WHEN]** .

1. Toccate il menu a discesa **[!UICONTROL Seleziona stato]** e selezionate **[!UICONTROL viene modificato]**.

   ![quando customeridischanged](assets/whencustomeridischanged.png)

   Nell&#39;istruzione **[!UICONTROL THEN]** , selezionare **[!UICONTROL Richiama servizio]** dal menu a discesa **[!UICONTROL Seleziona azione]** .

1. Passa da Editor **** visivo all&#39;Editor **** codice. Il controllo dell&#39;interruttore si trova sul lato destro della finestra. Viene aperto l’Editor di codice, con codice simile al seguente:

   ![editor di codice](assets/code-editor.png)

1. Sostituite la sezione della variabile di input con il seguente codice:

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. Sostituisci la sezione guidelib.dataIntegrationUtils.executeOperation (operationInfo, input, output) con il seguente codice:

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

1. Visualizzare l&#39;anteprima del modulo adattivo. Immetti un ID cliente errato. Viene visualizzato un messaggio di errore.

   ![display-validation-error](assets/display-validation-error.gif)

