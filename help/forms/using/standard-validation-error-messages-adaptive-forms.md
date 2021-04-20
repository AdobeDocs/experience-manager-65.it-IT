---
title: Messaggi di errore di convalida standard per i moduli adattivi
seo-title: Messaggi di errore di convalida standard per i moduli adattivi
description: Trasforma i messaggi di errore di convalida per i moduli adattivi in formato standard utilizzando gestori di errori personalizzati
seo-description: Trasforma i messaggi di errore di convalida per i moduli adattivi in formato standard utilizzando gestori di errori personalizzati
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 0%

---


# Messaggi di errore di convalida standard per i moduli adattivi {#standard-validation-error-messages}

I moduli adattivi convalidano gli input forniti nei campi in base a criteri di convalida predefiniti. I criteri di convalida si riferiscono ai valori di input accettabili per i campi in un modulo adattivo. È possibile impostare i criteri di convalida in base all’origine dati utilizzata con il modulo adattivo. Ad esempio, se utilizzi i servizi web RESTful come origine dati, puoi definire i criteri di convalida in un file di definizione Swagger.

Se i valori immessi soddisfano i criteri di convalida, questi vengono inviati all’origine dati. In caso contrario, nel modulo adattivo viene visualizzato un messaggio di errore.

Analogamente a questo approccio, i moduli adattivi possono ora integrarsi con i servizi personalizzati per eseguire le convalide dei dati. Se i valori di input non soddisfano i criteri di convalida e il messaggio di errore di convalida restituito dal server è nel formato di messaggio standard, i messaggi di errore vengono visualizzati a livello di campo nel modulo.

Se i valori di input non soddisfano i criteri di convalida e il messaggio di errore di convalida del server non è nel formato di messaggio standard, i moduli adattivi forniscono un meccanismo per trasformare i messaggi di errore di convalida in un formato standard in modo che vengano visualizzati a livello di campo nel modulo. Puoi trasformare il messaggio di errore nel formato standard utilizzando uno dei due metodi seguenti:

* Aggiungi un gestore di errori personalizzato per l’invio di moduli adattivi
* Aggiungi il gestore personalizzato all&#39;azione Invoke Service utilizzando l&#39;Editor regole

Questo articolo descrive il formato standard dei messaggi di errore convalida e le istruzioni per trasformare i messaggi di errore da un formato personalizzato a quello standard.

## Formato del messaggio di errore di convalida standard {#standard-validation-message-format}

Nei moduli adattivi vengono visualizzati gli errori a livello di campo se i messaggi di errore convalida del server sono nel seguente formato standard:

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
* `errors` menzione dell’espressione SOM dei campi che non hanno soddisfatto i criteri di convalida insieme al messaggio di errore di convalida
* `originCode` contiene il codice di errore restituito dal servizio esterno
* `originMessage` contiene i dati di errore non elaborati restituiti dal servizio esterno

## Configurare l’invio di moduli adattivi per aggiungere gestori personalizzati {#configure-adaptive-form-submission}

Se il messaggio di errore convalida server non viene visualizzato nel formato standard, è possibile abilitare l’invio asincrono e aggiungere un gestore di errori personalizzato nell’invio di moduli adattivi per convertire il messaggio in un formato standard.

### Configurare l’invio asincrono dei moduli adattivi {#configure-asynchronous-adaptive-form-submission}

Prima di aggiungere un gestore personalizzato, devi configurare il modulo adattivo per l’invio asincrono. Esegui i seguenti passaggi:

1. In modalità di creazione dei moduli adattivi, seleziona l’oggetto contenitore modulo e tocca ![proprietà dei moduli adattivi](assets/configure_icon.png) per aprire le relative proprietà.
1. Nella sezione delle proprietà **[!UICONTROL Invio]** , abilita **[!UICONTROL Usa invio asincrono]**.
1. Selezionare **[!UICONTROL Rivaluta sul server]** per convalidare i valori dei campi di input sul server prima dell&#39;invio.
1. Selezionare l’azione Invia:

   * Selezionare **[!UICONTROL Invia utilizzando Form Data Model]** e selezionare il modello dati appropriato, se si utilizza RESTful Web Service based [form data model](work-with-form-data-model.md) come origine dati.
   * Seleziona **[!UICONTROL Invia all&#39;endpoint REST]** e specifica l&#39; **[!UICONTROL URL/percorso di reindirizzamento]** se utilizzi i servizi web RESTful come origine dati.

   ![proprietà di invio del modulo adattivo](assets/af_submission_properties.png)

1. Tocca ![Salva](assets/save_icon.png) per salvare le proprietà.

### Aggiungi un gestore di errori personalizzato per l’invio di moduli adattivi {#add-custom-error-handler-af-submission}

AEM Forms fornisce gestori di errori e di successo preconfigurati per l’invio dei moduli. I gestori sono funzioni lato client che vengono eseguite in base alla risposta del server. Quando un modulo viene inviato, i dati vengono trasmessi al server per la convalida, che restituisce una risposta al client con informazioni sull’evento riuscito o di errore per l’invio. Le informazioni vengono passate come parametri al gestore pertinente per eseguire la funzione .

Esegui i seguenti passaggi per aggiungere un gestore di errori personalizzato all’invio di moduli adattivi:

1. Apri il modulo adattivo in modalità di creazione, seleziona un oggetto modulo qualsiasi e tocca <!--![Rule Editor](assets/af_edit_rules.png)--> per aprire l’editor di regole.
1. Selezionare **[!UICONTROL Modulo]** nella struttura Oggetti modulo e toccare **[!UICONTROL Crea]**.
1. Selezionare **[!UICONTROL Errore nell&#39;invio]** dall&#39;elenco a discesa Evento.
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

L’ `var som_map` elenca l’espressione SOM dei campi modulo adattivo che si desidera trasformare in formato standard. Per visualizzare l’espressione SOM di qualsiasi campo in un modulo adattivo, tocca il campo e seleziona **[!UICONTROL Visualizza espressione SOM]**.

Utilizzando questo gestore di errori personalizzato, il modulo adattivo converte i campi elencati in `var som_map` nel formato di messaggio di errore standard. Di conseguenza, i messaggi di errore di convalida vengono visualizzati a livello di campo nel modulo adattivo.

## Aggiungi un gestore personalizzato utilizzando l&#39;azione Invoke Service

Esegui i seguenti passaggi per aggiungere un gestore di errori per convertire una struttura di errore personalizzata nella struttura di errore standard utilizzando l&#39;azione [Editor di regole](rule-editor.md) Invoke Service:

1. Apri il modulo adattivo in modalità di authoring, seleziona un oggetto modulo qualsiasi e tocca ![Editor regole](assets/rule_editor_icon.png) per aprire l’editor di regole.
1. Tocca **[!UICONTROL Crea]**.
1. Crea una condizione nella sezione **[!UICONTROL When]** della regola. Ad esempio, se viene modificato [Nome del campo]. Seleziona **[!UICONTROL viene modificato]** dall&#39;elenco a discesa **[!UICONTROL Seleziona stato]** per ottenere questa condizione.
1. Nella sezione **[!UICONTROL Then]** , seleziona **[!UICONTROL Invoke Service]** dall&#39;elenco a discesa **[!UICONTROL Select Action]** .
1. Seleziona un servizio Post e i relativi binding dei dati dalla sezione **[!UICONTROL Input]** . Ad esempio, se desideri convalidare i campi **Name**, **ID** e **Status** nel modulo adattivo, seleziona un servizio Post (pet) e seleziona pet.name, pet.id e pet.status nella sezione **[!UICONTROL Input]**.

Come risultato di questa regola, i valori immessi per i campi **Name**, **ID** e **Status** vengono convalidati non appena il campo definito nel passaggio 2 viene modificato e si esce dal campo nel modulo.

1. Seleziona **[!UICONTROL Editor di codice]** dall&#39;elenco a discesa di selezione della modalità.
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

   L’ `var som_map` elenca l’espressione SOM dei campi modulo adattivo che si desidera trasformare in formato standard. Per visualizzare l’espressione SOM di qualsiasi campo in un modulo adattivo, tocca il campo e seleziona **[!UICONTROL Visualizza espressione SOM]** dal menu **[!UICONTROL Altre opzioni]** (...).

   Assicurati di copiare la seguente riga del codice di esempio nel gestore di errori personalizzato:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   L&#39;API executeOperation include i parametri `null` e `errorHandler` in base al nuovo gestore di errori personalizzato.

   Utilizzando questo gestore di errori personalizzato, il modulo adattivo converte i campi elencati in `var som_map` nel formato di messaggio di errore standard. Di conseguenza, i messaggi di errore di convalida vengono visualizzati a livello di campo nel modulo adattivo.