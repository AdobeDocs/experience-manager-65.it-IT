---
title: Personalizzazione del tracciamento degli eventi del modulo
seo-title: Customizing form event tracking
description: Se un utente trascorre più di 60 secondi su un campo, viene attivato un evento di visita del campo e i dettagli del campo vengono inviati ad Adobe SiteCatalyst.
seo-description: If a user spends more than 60 seconds on a field, a fieldvisit event is triggered and the details of the field are sent to Adobe SiteCatalyst.
uuid: 2f790085-2f1a-45be-9a69-6100c76dcae0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 60d67c6b-5994-42ef-b159-ed6edf5cf9d4
exl-id: d0280a15-5d0d-49cf-bce9-ad1c40530eae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 1%

---

# Personalizzazione del tracciamento degli eventi del modulo {#customizing-form-event-tracking}

I seguenti eventi vengono tracciati in un modulo adattivo abilitato per Analytics:

<table>
 <tbody>
  <tr>
   <th>Evento</th>
   <th>Variabili disponibili</th>
  </tr>
  <tr>
   <td>rendering</td>
   <td>formName, formTitle, formInstance, source</td>
  </tr>
  <tr>
   <td>abbandonare</td>
   <td>formName, formTitle, formInstance, panelName, panelTitle</td>
  </tr>
  <tr>
   <td>salva</td>
   <td>formName, formTitle, formInstance, panelName, source</td>
  </tr>
  <tr>
   <td>submit</td>
   <td>formName, formTitle, formInstance, source</td>
  </tr>
  <tr>
   <td>errore</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle</td>
  </tr>
  <tr>
   <td>Aiuto di </td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle</td>
  </tr>
  <tr>
   <td>fieldVisit</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle<br /> </td>
  </tr>
  <tr>
   <td>panelVisit</td>
   <td>formName, formTitle, panelName, panelTitle</td>
  </tr>
 </tbody>
</table>

## Personalizzazione del timeout dell’evento di visita del campo {#customizing-the-field-visit-event-timeout}

Nella configurazione predefinita del modulo AEM, se un utente spende più di 60 secondi su un campo, viene visualizzata una `fieldvisit` viene attivato e i dettagli del campo vengono inviati ad Adobe Analytics. Puoi personalizzare la linea di base per il tracciamento dell’ora del campo in Configurazione di AEM Forms Analytics AEM console di configurazione (/system/console/configMgr) per aumentare o diminuire il limite di timeout.

## Personalizzazione degli eventi di tracciamento {#customizing-the-tracking-events}

Puoi modificare la `trackEvent`funzione disponibile in `/libs/afanalytics/js/custom.js` per personalizzare il tracciamento degli eventi. Ogni volta che un evento in corso di tracciamento si verifica in un modulo adattivo, il `trackEvent`viene chiamata la funzione . La `trackEvent` La funzione accetta due parametri: `eventName`e `variableValueMap`.

Puoi valutare il valore di *eventName* e *variableValueMap* argomenti per modificare il comportamento di tracciamento degli eventi. Ad esempio, puoi scegliere di inviare le informazioni al server di analytics dopo che si è verificato un certo numero di eventi di errore. Puoi anche scegliere di eseguire una delle seguenti personalizzazioni:

* Puoi impostare una soglia temporale prima di inviare l’evento.
* È possibile mantenere uno stato per decidere l’azione, ad esempio *fieldVisit* invia un evento fittizio in base alla marca temporale dell’ultimo evento.
* È possibile utilizzare `pushEvent` funzione per inviare l’evento al server di analytics *.*

* Puoi scegliere di non inviare l’evento al server di analytics.

### Esempi {#sample}

Nell’esempio seguente, imposta lo stato per *errore* evento *fieldName* l&#39;attributo viene mantenuto. L’evento viene inviato al server di analisi solo se si verifica nuovamente un errore.

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## Personalizzazione dell’evento panelvisit {#customizing-the-panelvisit-event}

Nella configurazione predefinita di AEM Forms, dopo 60 secondi, viene controllato se la finestra contenente il modulo adattivo è attiva. Se la finestra è attiva, un `panelVisit`viene attivato in Adobe Analytics. Consente di verificare che il documento o il modulo sia attivo e di calcolare il tempo impiegato per il modulo o il documento corrispondente.

>[!NOTE]
>
>Il nome dell’evento utilizzato per tenere traccia dell’attività e del tempo trascorso è &quot;panelVisit&quot;. Questo evento è diverso dall’evento di visita del pannello elencato nella tabella precedente.

Puoi modificare la funzione ScheduleHeartBeatCheck disponibile nella `/libs/afanalytics/js/custom.js` per modificare o interrompere l’evento inviato ad Adobe Analytics a intervalli regolari.
