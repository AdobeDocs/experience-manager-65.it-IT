---
title: Messaggi di errore di convalida standard per i moduli adattivi
seo-title: Standard validation error messages for adaptive forms
description: Trasforma i messaggi di errore di convalida per i moduli adattivi in formato standard utilizzando gestori di errori personalizzati
seo-description: Transform the validation error messages for adaptive forms into standard format using custom error handlers
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
feature: Adaptive Forms
exl-id: 54a76d5c-d19b-4026-b71c-7b9e862874bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 0%

---

# Messaggi di errore di convalida standard per i moduli adattivi {#standard-validation-error-messages}

I moduli adattivi convalidano gli input forniti nei campi in base a criteri di convalida preimpostati. I criteri di convalida si riferiscono ai valori di input accettabili per i campi di un modulo adattivo. È possibile impostare i criteri di convalida in base all’origine dati utilizzata con il modulo adattivo. Ad esempio, se utilizzi i servizi web RESTful come origine dati, puoi definire i criteri di convalida in un file di definizione Swagger.

Se i valori di input soddisfano i criteri di convalida, vengono inviati all&#39;origine dati. In caso contrario, nel modulo adattivo viene visualizzato un messaggio di errore.

Simile a questo approccio, i moduli adattivi possono ora integrarsi con i servizi personalizzati per eseguire le convalide dei dati. Se i valori di input non soddisfano i criteri di convalida e il messaggio di errore di convalida restituito dal server è nel formato di messaggio standard, i messaggi di errore vengono visualizzati a livello di campo nel modulo.

Se i valori di input non soddisfano i criteri di convalida e il messaggio di errore di convalida del server non è nel formato di messaggio standard, i moduli adattivi forniscono un meccanismo per trasformare i messaggi di errore di convalida in un formato standard in modo che vengano visualizzati a livello di campo nel modulo. È possibile trasformare il messaggio di errore nel formato standard utilizzando uno dei due metodi seguenti:

* Aggiungi gestore errori personalizzato all’invio di moduli adattivi
* Aggiungere un gestore personalizzato per richiamare l’azione del servizio tramite l’editor di regole

Questo articolo descrive il formato standard per i messaggi di errore di convalida e le istruzioni per trasformare i messaggi di errore da un formato personalizzato a uno standard.

## Formato del messaggio di errore di convalida standard {#standard-validation-message-format}

I moduli adattivi visualizzano gli errori a livello di campo se i messaggi di errore di convalida del server sono nel seguente formato standard:

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             somExpression  : <somexpr>
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]

        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
}
```

Dove:

* `errorCausedBy` descrive il motivo dell’errore
* `errors` menziona l’espressione SOM dei campi che non hanno soddisfatto i criteri di convalida insieme al messaggio di errore di convalida
* `originCode` contiene il codice di errore restituito dal servizio esterno
* `originMessage` contiene i dati di errore non elaborati restituiti dal servizio esterno

## Configurare l’invio di moduli adattivi per aggiungere gestori personalizzati {#configure-adaptive-form-submission}

Se il messaggio di errore di convalida del server non viene visualizzato nel formato standard, puoi abilitare l’invio asincrono e aggiungere un gestore degli errori personalizzato all’invio del modulo adattivo per convertire il messaggio in formato standard.

### Configurare l’invio asincrono dei moduli adattivi {#configure-asynchronous-adaptive-form-submission}

Prima di aggiungere un gestore personalizzato, devi configurare il modulo adattivo per l’invio asincrono. Esegui i seguenti passaggi:

1. In modalità di authoring di moduli adattivi, seleziona l’oggetto Contenitore modulo e tocca ![proprietà modulo adattivo](assets/configure_icon.png) per aprirne le proprietà.
1. In **[!UICONTROL Invio]** proprietà, abilita **[!UICONTROL Utilizzare l’invio asincrono]**.
1. Seleziona **[!UICONTROL Riconvalida sul server]** per convalidare i valori dei campi di input sul server prima dell’invio.
1. Selezionare l&#39;azione di invio:

   * Seleziona **[!UICONTROL Invia utilizzando il modello dati modulo]** e seleziona il modello dati appropriato, se utilizzi il servizio web RESTful basato su [modello dati modulo](work-with-form-data-model.md) come origine di dati.
   * Seleziona **[!UICONTROL Invia all’endpoint REST]** e specificare **[!UICONTROL URL/percorso di reindirizzamento]**, se utilizzi i servizi web RESTful come origine di dati.

   ![proprietà di invio di moduli adattivi](assets/af_submission_properties.png)

1. Tocca ![Salva](assets/save_icon.png) per salvare le proprietà.

### Aggiungi gestore errori personalizzato all’invio di moduli adattivi {#add-custom-error-handler-af-submission}

AEM Forms fornisce gestori predefiniti di successo e di errori per l’invio di moduli. I gestori sono funzioni lato client che vengono eseguite in base alla risposta del server. Quando un modulo viene inviato, i dati vengono trasmessi al server per la convalida, che restituisce una risposta al client con informazioni sull’evento di successo o errore per l’invio. Le informazioni vengono passate come parametri al gestore pertinente per eseguire la funzione.

Per aggiungere un gestore di errori personalizzato all’invio di un modulo adattivo, effettua le seguenti operazioni:

1. Apri il modulo adattivo in modalità di authoring, seleziona un oggetto modulo qualsiasi e tocca <!--![Rule Editor](assets/af_edit_rules.png)--> per aprire l’editor di regole.
1. Seleziona **[!UICONTROL Modulo]** nella struttura Oggetti modulo e tocca **[!UICONTROL Crea]**.
1. Seleziona **[!UICONTROL Errore nell’invio]** dall’elenco a discesa Evento.
1. Scrivi una regola per convertire la struttura di errore personalizzata nella struttura di errore standard e tocca **[!UICONTROL Fine]** per salvare la regola.

Di seguito è riportato un codice di esempio per convertire una struttura di errore personalizzata nella struttura di errore standard:

```javascript
var data = $event.data;
var som_map = {
    "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
    "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
    "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
};

var errorJson = {};
errorJson.errors = [];

if (data) {
    if (data.originMessage) {
        var errorData;
        try {
            errorData = JSON.parse(data.originMessage);
        } catch (err) {
            // not in json format
        }

        if (errorData) {
            Object.keys(errorData).forEach(function(key) {
                var som_key = som_map[key];
                if (som_key) {
                    var error = {};
                    error.somExpression = som_key;
                    error.errorMessage = errorData[key];
                    errorJson.errors.push(error);
                }
            });
        }
        window.guideBridge.handleServerValidationError(errorJson);
    } else {
        window.guideBridge.handleServerValidationError(data);
    }
}
```

Il `var som_map` elenca l’espressione SOM dei campi del modulo adattivo che desideri trasformare nel formato standard. Per visualizzare l’espressione SOM di qualsiasi campo in un modulo adattivo, tocca il campo e seleziona **[!UICONTROL Visualizza espressione SOM]**.

Utilizzando questo gestore di errori personalizzato, il modulo adattivo converte i campi elencati in `var som_map` nel formato standard dei messaggi di errore. Di conseguenza, i messaggi di errore di convalida vengono visualizzati a livello di campo nel modulo adattivo.

## Aggiungi gestore personalizzato tramite l’azione Richiama servizio

Esegui la procedura seguente per aggiungere un gestore degli errori e convertire una struttura degli errori personalizzata nella struttura degli errori standard tramite [Dell&#39;editor di regole](rule-editor.md) Richiama azione servizio:

1. Apri il modulo adattivo in modalità di authoring, seleziona un oggetto modulo qualsiasi e tocca ![Editor regole](assets/rule_editor_icon.png) per aprire l’editor di regole.
1. Tocca **[!UICONTROL Crea]**.
1. Creare una condizione in **[!UICONTROL Quando]** sezione della regola. Ad esempio, Quando[Nome del campo] è stato modificato. Seleziona **[!UICONTROL è stato modificato]** dal **[!UICONTROL Seleziona stato]** per ottenere questa condizione.
1. In **[!UICONTROL Then]** sezione, seleziona **[!UICONTROL Richiama servizio]** dal **[!UICONTROL Seleziona azione]** elenco a discesa.
1. Seleziona un servizio di post e le associazioni dati corrispondenti dalla sezione **[!UICONTROL Input]** sezione. Ad esempio, se desideri convalidare **Nome**, **ID**, e **Stato** nel modulo adattivo, seleziona un servizio di post (pet) e seleziona pet.name, pet.id e pet.status nel **[!UICONTROL Input]** sezione.

Come risultato di questa regola, i valori immessi per **Nome**, **ID**, e **Stato** I campi vengono convalidati, non appena il campo definito nel passaggio 2 viene modificato e si esce dal campo nel modulo.

1. Seleziona **[!UICONTROL Editor di codice]** dall’elenco a discesa selezione modalità.
1. Tocca **[!UICONTROL Modifica codice]**.
1. Elimina la riga seguente dal codice esistente:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
   ```

1. Scrivi una regola per convertire la struttura di errore personalizzata nella struttura di errore standard e tocca **[!UICONTROL Fine]** per salvare la regola.
Ad esempio, aggiungi il seguente codice di esempio alla fine per convertire una struttura di errore personalizzata nella struttura di errore standard:

   ```javascript
   var errorHandler = function(jqXHR, data) {
   var som_map = {
       "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
       "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
       "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
   };
   
   
   var errorJson = {};
   errorJson.errors = [];
   
   if (data) {
       if (data.originMessage) {
           var errorData;
           try {
               errorData = JSON.parse(data.originMessage);
           } catch (err) {
               // not in json format
           }
   
           if (errorData) {
               Object.keys(errorData).forEach(function(key) {
                   var som_key = som_map[key];
                   if (som_key) {
                       var error = {};
                       error.somExpression = som_key;
                       error.errorMessage = errorData[key];
                       errorJson.errors.push(error);
                   }
               });
           }
           window.guideBridge.handleServerValidationError(errorJson);
       } else {
           window.guideBridge.handleServerValidationError(data);
       }
     }
   };
   
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   Il `var som_map` elenca l’espressione SOM dei campi del modulo adattivo che desideri trasformare nel formato standard. Per visualizzare l’espressione SOM di qualsiasi campo in un modulo adattivo, tocca il campo e seleziona **[!UICONTROL Visualizza espressione SOM]** da **[!UICONTROL Altre opzioni]** (...).

   Assicurati di copiare la seguente riga del codice di esempio nel gestore degli errori personalizzato:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   L&#39;API executeOperation include `null` e `errorHandler` parametri basati sul nuovo gestore degli errori personalizzato.

   Utilizzando questo gestore di errori personalizzato, il modulo adattivo converte i campi elencati in `var som_map` nel formato standard dei messaggi di errore. Di conseguenza, i messaggi di errore di convalida vengono visualizzati a livello di campo nel modulo adattivo.
