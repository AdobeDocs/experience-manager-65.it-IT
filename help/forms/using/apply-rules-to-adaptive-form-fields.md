---
title: Applicazione di regole ai campi del modulo adattivo
seo-title: Apply rules to adaptive form fields
description: Creare regole per aggiungere interattività, logica di business e convalide avanzate a un modulo adattivo.
seo-description: Create rules to add interactivity, business logic, and smart validations to an adaptive form.
page-status-flag: de-activated
uuid: 60f142aa-81ca-4333-8614-85a01e23e917
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 982eddba-2350-40e7-8a42-db02d28cf133
exl-id: 0202ca65-21ef-4477-b704-7b52314a7d7b
source-git-commit: 63bc43bba88a42d62fb574bc8ce42470ac61d693
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 0%

---

# Esercitazione: Applicazione di regole ai campi del modulo adattivo {#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

Questa esercitazione è un passaggio nel [Creare il primo modulo adattivo](/help/forms/using/create-your-first-adaptive-form.md) serie. Adobe consiglia di seguire le serie in sequenza cronologica per comprendere, eseguire e illustrare il caso d’uso completo dell’esercitazione.

## Informazioni sull’esercitazione {#about-the-tutorial}

Puoi utilizzare le regole per aggiungere interattività, logica di business e convalide avanzate a un modulo adattivo. I moduli adattivi dispongono di un editor di regole integrato. L’editor di regole fornisce una funzionalità di trascinamento della selezione, simile alle visite guidate. Il metodo di trascinamento della selezione è il metodo più veloce e facile per creare regole. L&#39;editor di regole fornisce anche una finestra di codice per gli utenti interessati a testare le proprie capacità di codifica o a portare le regole al livello successivo.

Per ulteriori informazioni sull’editor di regole, consulta [Editor di regole Forms adattivo](/help/forms/using/rule-editor.md).

Al termine dell’esercitazione, imparerai a creare regole per:

* Richiamare un servizio Form Data Model per recuperare i dati dal database
* Richiamare un servizio Form Data Model per aggiungere dati al database
* Esegui un controllo di convalida e visualizza messaggi di errore

Le immagini interattive di GIF alla fine di ogni sezione dell’esercitazione consentono di apprendere e convalidare al volo la funzionalità del modulo che si sta creando.

## Passaggio 1: Recupera un record cliente dal database {#retrieve-customer-record}

È stato creato un modello dati modulo seguendo la procedura descritta di seguito [creare un modello dati modulo](/help/forms/using/create-form-data-model.md) articolo. Ora è possibile utilizzare l’editor di regole per richiamare i servizi Forms Data Model per recuperare e aggiungere informazioni al database.

A ogni cliente viene assegnato un numero ID cliente univoco, che consente di identificare i dati cliente rilevanti in un database. La procedura seguente utilizza l&#39;ID cliente per recuperare le informazioni dal database:

1. Apri il modulo adattivo per la modifica.

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. Tocca **[!UICONTROL ID cliente]** e tocca **[!UICONTROL Modifica regole]** icona. Viene visualizzata la finestra Editor regole.
1. Tocca **[!UICONTROL + Crea]** per aggiungere una regola. Apre l&#39;Editor visivo.

   Nell&#39;Editor visivo, la **[!UICONTROL QUANDO]** istruzione è selezionata per impostazione predefinita. Inoltre, l&#39;oggetto modulo (in questo caso, **[!UICONTROL ID cliente]**) da dove hai avviato l&#39;editor di regole viene specificato nella sezione **[!UICONTROL QUANDO]** istruzione.

1. Tocca **[!UICONTROL Seleziona stato]** a discesa e seleziona **[!UICONTROL viene modificato]**.

   ![quando customeridischanged](assets/whencustomeridischanged.png)

1. In **[!UICONTROL POI]** istruzione, seleziona **[!UICONTROL Richiama servizio]** dal **[!UICONTROL Seleziona azione]** a discesa.
1. Seleziona la **[!UICONTROL Recupera indirizzo di spedizione]** dal servizio **[!UICONTROL Seleziona]** a discesa.
1. Trascina e rilascia la **[!UICONTROL ID cliente]** dalla scheda Oggetti modulo al campo **[!UICONTROL Rilascia oggetto o seleziona qui]** nel campo **[!UICONTROL INGRESSO]** scatola.

   ![dropobjectstoinputfield-retrievedata](assets/dropobjectstoinputfield-retrievedata.png)

1. Trascina e rilascia la **[!UICONTROL ID cliente, nome, indirizzo di spedizione, stato e codice postale]** dalla scheda Oggetti modulo al campo **[!UICONTROL Rilascia oggetto o seleziona qui]** nel campo **[!UICONTROL USCITA]** scatola.

   ![dropobjectstooutputfield-retrievedata](assets/dropobjectstooutputfield-retrievedata.png)

   Tocca **[!UICONTROL Fine]** per salvare la regola. Nella finestra dell’editor delle regole, tocca **[!UICONTROL Chiudi]**.

1. Visualizzare l’anteprima del modulo adattivo. Immetti un ID nel **[!UICONTROL ID cliente]** campo . Il modulo ora può recuperare i dettagli dei clienti dal database.

   ![recupero-informazioni](assets/retrieve-information.gif)

## Passaggio 2: Aggiungi l&#39;indirizzo cliente aggiornato al database {#updated-customer-address}

Una volta recuperati i dettagli del cliente dal database, puoi aggiornare l’indirizzo di spedizione, lo stato e il codice postale. La procedura seguente richiama un servizio Form Data Model per aggiornare le informazioni dei clienti al database:

1. Seleziona la **[!UICONTROL Invia]** e tocca **[!UICONTROL Modifica regole]** icona. Viene visualizzata la finestra Editor regole.
1. Seleziona la **[!UICONTROL Invia - Fai clic]** e tocca **[!UICONTROL Modifica]** icona. Vengono visualizzate le opzioni per modificare la regola di invio.

   ![regola di invio](assets/submit-rule.png)

   Nell’opzione WHEN (QUANDO), la **[!UICONTROL Invia]** e **[!UICONTROL è selezionato]** le opzioni sono già selezionate.

   ![invia con un clic](assets/submit-is-clicked.png)

1. In **[!UICONTROL POI]** , tocca **[!UICONTROL + Aggiungi istruzione]** opzione . Seleziona **[!UICONTROL Richiama servizio]** dal **[!UICONTROL Seleziona azione]** a discesa.
1. Seleziona la **[!UICONTROL Aggiorna indirizzo di spedizione]** dal servizio **[!UICONTROL Seleziona]** a discesa.

   ![indirizzo di spedizione-aggiornamento](assets/update-shipping-address.png)

   ![dropobjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. Trascina e rilascia la **[!UICONTROL Indirizzo di spedizione, Stato e CAP]** dal campo [!UICONTROL Oggetti modulo] alla corrispondente tabella.property (ad esempio, customerdetails .shippingAddress) del **[!UICONTROL Rilascia oggetto o seleziona qui]** nel campo **[!UICONTROL INGRESSO]** scatola. Tutti i campi con prefisso nome tabella (ad esempio, dettagli cliente in questo caso d’uso) fungono da dati di input per il servizio di aggiornamento. Tutto il contenuto fornito in questi campi viene aggiornato nell’origine dati.

   >[!NOTE]
   >
   >Non trascinare il **[!UICONTROL Nome]** e **[!UICONTROL ID cliente]** alla corrispondente tablespace.property (ad esempio, customerdetails.name). Aiuta ad evitare di aggiornare per errore nome e ID del cliente.

1. Trascina e rilascia la **[!UICONTROL ID cliente]** dal campo [!UICONTROL Oggetti modulo] al campo id nel **[!UICONTROL INGRESSO]** scatola. I campi senza nome tabella prefisso (ad esempio, dettagli cliente in questo caso d’uso) fungono da parametro di ricerca per il servizio di aggiornamento. La **[!UICONTROL id]** in questo caso d&#39;uso identifica in modo univoco un record nel  **dettagli cliente**  tabella.
1. Tocca **[!UICONTROL Fine]** per salvare la regola. Nella finestra dell’editor delle regole, tocca **[!UICONTROL Chiudi]**.
1. Visualizzare l’anteprima del modulo adattivo. Recupera i dettagli di un cliente, aggiorna l’indirizzo di spedizione e invia il modulo. Quando recuperi nuovamente i dettagli dello stesso cliente, viene visualizzato l&#39;indirizzo di spedizione aggiornato.

## Passaggio 3: (sezione Bonus) Utilizza l’editor di codice per eseguire convalide e visualizzare messaggi di errore {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

È necessario eseguire la convalida del modulo per verificare che i dati immessi nel modulo siano corretti e che venga visualizzato un messaggio di errore in caso di dati errati. Ad esempio, se nel modulo viene immesso un ID cliente non esistente, deve essere visualizzato un messaggio di errore.

I moduli adattivi forniscono diversi componenti con convalide integrate, ad esempio campi e-mail e numerici da utilizzare in casi d’uso comuni. Utilizza l&#39;editor di regole per i casi d&#39;uso avanzati, ad esempio, per visualizzare un messaggio di errore quando il database restituisce zero (0) record (nessun record).

La procedura seguente mostra come creare una regola per visualizzare un messaggio di errore se l’ID cliente immesso nel modulo non esiste nel database. La regola inoltre attiva e reimposta la **[!UICONTROL ID cliente]** campo . La regola utilizza [API dataIntegrationUtils del servizio del modello dati del modulo](/help/forms/using/invoke-form-data-model-services.md) per verificare se l&#39;ID cliente esiste nel database.

1. Tocca **[!UICONTROL ID cliente]** e tocca `Edit Rules` icona. La [!UICONTROL Editor regole] si apre la finestra.
1. Tocca **[!UICONTROL + Crea]** per aggiungere una regola. Apre l&#39;Editor visivo.

   Nell&#39;Editor visivo, la **[!UICONTROL QUANDO]** istruzione è selezionata per impostazione predefinita. Inoltre, l&#39;oggetto modulo (in questo caso, **[!UICONTROL ID cliente]**) da dove hai avviato l&#39;editor di regole viene specificato nella sezione **[!UICONTROL QUANDO]** istruzione.

1. Tocca **[!UICONTROL Seleziona stato]** a discesa e seleziona **[!UICONTROL viene modificato]**.

   ![quando customeridischanged](assets/whencustomeridischanged.png)

   In **[!UICONTROL POI]** istruzione, seleziona **[!UICONTROL Richiama servizio]** dal **[!UICONTROL Seleziona azione]** a discesa.

1. Passa da **[!UICONTROL Editor visivo]** a **[!UICONTROL Editor di codice]**. Il controllo dell&#39;interruttore si trova sul lato destro della finestra. Viene aperto l’Editor di codice, con codice simile al seguente:

   ![editor di codice](assets/code-editor.png)

1. Sostituisci la sezione della variabile di input con il seguente codice:

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. Sostituisci il `guidelib.dataIntegrationUtils.executeOperation (operationInfo, inputs, outputs)` con il seguente codice:

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

1. Visualizzare l’anteprima del modulo adattivo. Immetti un ID cliente errato. Viene visualizzato un messaggio di errore.

   ![display-validation-error](assets/display-validation-error.gif)
