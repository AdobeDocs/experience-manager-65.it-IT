---
title: Messaggi di errore di convalida standard per i moduli adattivi
seo-title: Messaggi di errore di convalida standard per i moduli adattivi
description: Trasforma i messaggi di errore convalida per i moduli adattivi in formato standard utilizzando gestori di errori personalizzati
seo-description: Trasforma i messaggi di errore convalida per i moduli adattivi in formato standard utilizzando gestori di errori personalizzati
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 0%

---


# Messaggi di errore di convalida standard per i moduli adattivi {#standard-validation-error-messages}

I moduli adattivi convalidano gli input forniti nei campi in base a criteri di convalida predefiniti. I criteri di convalida fanno riferimento ai valori di input accettabili per i campi di un modulo adattivo. È possibile impostare i criteri di convalida in base all&#39;origine dati utilizzata con il modulo adattivo. Ad esempio, se si utilizzano i servizi Web RESTful come origine dati, è possibile definire i criteri di convalida in un file di definizione Swagger.

Se i valori immessi soddisfano i criteri di convalida, i valori vengono inviati all&#39;origine dati. In caso contrario, nel modulo adattivo viene visualizzato un messaggio di errore.

Come per questo approccio, i moduli adattivi possono ora integrarsi con i servizi personalizzati per eseguire le convalide dei dati. Se i valori di input non soddisfano i criteri di convalida e il messaggio di errore di convalida restituito dal server è nel formato di messaggio standard, i messaggi di errore vengono visualizzati a livello di campo nel modulo.

Se i valori di input non soddisfano i criteri di convalida e il messaggio di errore convalida server non è nel formato di messaggio standard, i moduli adattivi forniscono un meccanismo per trasformare i messaggi di errore di convalida in un formato standard in modo che siano visualizzati a livello di campo nel modulo. Potete trasformare il messaggio di errore nel formato standard utilizzando uno dei due metodi seguenti:

* Aggiunta di un gestore errori personalizzato per l&#39;invio di moduli adattivi
* Aggiunta di un gestore personalizzato all&#39;azione di richiamo del servizio tramite Editor regole

Questo articolo descrive il formato standard dei messaggi di errore convalida e le istruzioni per trasformare i messaggi di errore da un formato personalizzato a quello standard.

## Formato del messaggio di errore convalida standard {#standard-validation-message-format}

Nei moduli adattivi sono visualizzati gli errori a livello di campo se i messaggi di errore convalida server sono nel seguente formato standard:

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

* `errorCausedBy` descrive il motivo dell&#39;errore
* `errors` menzionare l&#39;espressione SOM dei campi che non hanno soddisfatto i criteri di convalida insieme al messaggio di errore di convalida
* `originCode` contiene il codice di errore restituito dal servizio esterno
* `originMessage` contiene i dati di errore non elaborati restituiti dal servizio esterno

## Configurare l&#39;invio di moduli adattivi per l&#39;aggiunta di gestori personalizzati {#configure-adaptive-form-submission}

Se il messaggio di errore convalida server non è visualizzato nel formato standard, è possibile abilitare l&#39;invio asincrono e aggiungere un gestore errori personalizzato per l&#39;invio di moduli adattivi per convertire il messaggio in un formato standard.

### Configurare l&#39;invio asincrono di moduli adattivi {#configure-asynchronous-adaptive-form-submission}

Prima di aggiungere un gestore personalizzato, è necessario configurare il modulo adattivo per l&#39;invio asincrono. Effettuate i seguenti passaggi:

1. In modalità di creazione moduli adattivi, selezionare l&#39;oggetto Contenitore modulo e toccare le proprietà ![del modulo](assets/configure_icon.png) adattivo per aprirne le proprietà.
1. Nella sezione Proprietà **[!UICONTROL invio]** , abilitare **[!UICONTROL Usa invio]** asincrono.
1. Selezionare **[!UICONTROL Revoca sul server]** per convalidare i valori dei campi di input sul server prima dell&#39;invio.
1. Selezionate l’azione Invia:

   * Selezionare **[!UICONTROL Invia utilizzando il modello]** dati modulo e selezionare il modello dati appropriato, se si utilizza il modello [dati](work-with-form-data-model.md) modulo basato su servizi Web RESTful come origine dati.
   * Selezionare **[!UICONTROL Invia a endpoint]** REST e specificare l&#39;URL/percorso **[!UICONTROL di]** reindirizzamento se si utilizzano i servizi Web RESTful come origine dati.

   ![proprietà di invio dei moduli adattivi](assets/af_submission_properties.png)

1. Toccate ![Salva](assets/save_icon.png) per salvare le proprietà.

### Aggiunta di un gestore errori personalizzato per l&#39;invio di moduli adattivi {#add-custom-error-handler-af-submission}

I AEM Forms forniscono gestori di errori e di successo out-of-the-box per l&#39;invio dei moduli. I gestori sono funzioni lato client che vengono eseguite in base alla risposta del server. Quando un modulo viene inviato, i dati vengono trasmessi al server per la convalida, che restituisce una risposta al client con informazioni sull&#39;evento success o error per l&#39;invio. Le informazioni vengono trasmesse come parametri al gestore interessato per eseguire la funzione.

Per aggiungere un gestore errori personalizzato all&#39;invio di moduli adattivi, eseguire i passaggi seguenti:

1. Aprite il modulo adattivo in modalità di creazione, selezionate un oggetto modulo qualsiasi e toccate <!--![Rule Editor](assets/af_edit_rules.png)--> per aprire l&#39;editor delle regole.
1. Selezionare **[!UICONTROL Modulo]** nella struttura Oggetti modulo e toccare **[!UICONTROL Crea]**.
1. Selezionare **[!UICONTROL Errore nell&#39;invio]** dall&#39;elenco a discesa Evento.
1. Scrivete una regola per convertire la struttura di errore personalizzata nella struttura di errore standard e toccate **[!UICONTROL Fine]** per salvare la regola.

Di seguito è riportato un esempio di codice per convertire una struttura di errore personalizzata nella struttura di errore standard:

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

L&#39; `var som_map` elenco elenca l&#39;espressione SOM dei campi modulo adattivi che si desidera trasformare nel formato standard. Per visualizzare l&#39;espressione SOM di qualsiasi campo in un modulo adattivo, toccate il campo e selezionate **[!UICONTROL Visualizza espressione]** SOM.

Utilizzando questo handler di errori personalizzato, il modulo adattivo converte i campi elencati nel formato `var som_map` di messaggio di errore standard. Di conseguenza, i messaggi di errore convalida vengono visualizzati a livello di campo nel modulo adattivo.

## Aggiunta di un gestore personalizzato tramite l&#39;azione Servizio di chiamata

Per aggiungere un gestore di errori per convertire una struttura di errore personalizzata nella struttura di errore standard, eseguire la procedura seguente utilizzando l&#39;azione Servizio di chiamata dell&#39;Editor di [regole](rule-editor.md) :

1. Aprite il modulo adattivo in modalità di creazione, selezionate un oggetto modulo qualsiasi e toccate Editor ![](assets/rule_editor_icon.png) regole per aprire l&#39;editor di regole.
1. Toccate **[!UICONTROL Crea]**.
1. Creare una condizione nella sezione **[!UICONTROL Quando]** della regola. Ad esempio,[QuandoName del campo] viene modificato. Selezionate **[!UICONTROL viene modificato]** dall’elenco a discesa **[!UICONTROL Seleziona stato]** per ottenere questa condizione.
1. Nella sezione **[!UICONTROL Quindi]** , selezionare **[!UICONTROL Richiama servizio]** dall&#39;elenco a discesa **[!UICONTROL Seleziona azione]** .
1. Selezionare un servizio Post e i relativi binding dei dati dalla sezione **[!UICONTROL Input]** . Ad esempio, se si desidera convalidare i campi **Nome**, **ID** e **Stato** nel modulo adattivo, selezionare un servizio Post (animale domestico) e quindi pet.name, pet.id e pet.status nella sezione **[!UICONTROL Input]** .

Come risultato di questa regola, i valori inseriti per i campi **Nome**, **ID** e **Stato** vengono convalidati non appena il campo definito al punto 2 viene modificato e si esce dal campo del modulo.

1. Selezionare Editor **[!UICONTROL di]** codice dall&#39;elenco a discesa di selezione della modalità.
1. Toccate **[!UICONTROL Modifica codice]**.
1. Elimina la riga seguente dal codice esistente:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
   ```

1. Scrivete una regola per convertire la struttura di errore personalizzata nella struttura di errore standard e toccate **[!UICONTROL Fine]** per salvare la regola.
Ad esempio, aggiungete il seguente codice di esempio alla fine per convertire una struttura di errore personalizzata nella struttura di errore standard:

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

   L&#39; `var som_map` elenco elenca l&#39;espressione SOM dei campi modulo adattivi che si desidera trasformare nel formato standard. Per visualizzare l&#39;espressione SOM di qualsiasi campo in un modulo adattivo, toccate il campo e selezionate **[!UICONTROL Visualizza espressione]** SOM dal menu **[!UICONTROL Altre opzioni]** (...).

   Assicurarsi di copiare la riga seguente del codice di esempio nel gestore errori personalizzato:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   L&#39;API executeOperation include i `null` parametri e `errorHandler` i parametri basati sul nuovo gestore di errori personalizzato.

   Utilizzando questo handler di errori personalizzato, il modulo adattivo converte i campi elencati nel formato `var som_map` di messaggio di errore standard. Di conseguenza, i messaggi di errore convalida vengono visualizzati a livello di campo nel modulo adattivo.