---
title: Personalizzazione del tracciamento degli eventi modulo
seo-title: Personalizzazione del tracciamento degli eventi modulo
description: Se un utente trascorre più di 60 secondi su un campo, viene attivato un evento field visit e i dettagli del campo vengono inviati ad Adobe SiteCatalyst.
seo-description: Se un utente trascorre più di 60 secondi su un campo, viene attivato un evento field visit e i dettagli del campo vengono inviati ad Adobe SiteCatalyst.
uuid: 2f790085-2f1a-45be-9a69-6100c76dcae0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 60d67c6b-5994-42ef-b159-ed6edf5cf9d4
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---


# Personalizzazione del tracciamento degli eventi modulo {#customizing-form-event-tracking}

In un modulo adattivo abilitato per l&#39;analisi, vengono tracciati gli eventi seguenti:

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
   <td>abbandono</td>
   <td>formName, formTitle, formInstance, panelName, panelTitle</td>
  </tr>
  <tr>
   <td>save</td>
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
   <td>aiuto</td>
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

## Personalizzazione del timeout dell’evento visita sul campo {#customizing-the-field-visit-event-timeout}

Nella configurazione predefinita del modulo AEM, se un utente trascorre più di 60 secondi su un campo, viene attivato un `fieldvisit` evento e i dettagli del campo vengono inviati ad Adobe  Analytics. Puoi personalizzare la linea di base per il tracciamento dell’ora del campo in AEM Forms  configurazione Analytics nella console di configurazione AEM (/system/console/configMgr) per aumentare o diminuire il limite di timeout.

## Personalizzazione degli eventi di tracciamento {#customizing-the-tracking-events}

Potete modificare la `trackEvent`funzione disponibile nel `/libs/afanalytics/js/custom.js` file per personalizzare il tracciamento dell&#39;evento. Ogni volta che si verifica un evento in corso di tracciamento in un modulo adattivo, viene chiamata la `trackEvent`funzione. La `trackEvent` funzione accetta due parametri: `eventName`e `variableValueMap`.

È possibile valutare il valore degli argomenti *eventName* e *variableValueMap* per modificare il comportamento di tracciamento degli eventi. Ad esempio, potete scegliere di inviare le informazioni al server di analisi dopo un certo numero di eventi di errore. Potete anche scegliere di eseguire una delle seguenti personalizzazioni:

* Potete impostare un&#39;ora di soglia prima di inviare l&#39;evento.
* È possibile mantenere uno stato per decidere l&#39;azione, ad esempio *fieldVisit* , che invia un evento fittizio in base alla marca temporale dell&#39;ultimo evento.
* Potete utilizzare la `pushEvent` funzione per inviare l&#39;evento al server di analisi *.*

* Potete scegliere di non inviare l&#39;evento al server di analisi.

### Esempi {#sample}

Nell&#39;esempio seguente, lo stato per l&#39;evento *error* di ogni attributo *fieldName* viene mantenuto. L&#39;evento viene inviato al server di analisi solo se si verifica di nuovo un errore.

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## Personalizzazione dell’evento panelvisit {#customizing-the-panelvisit-event}

Nella configurazione dei AEM Forms predefiniti, dopo 60 secondi, viene verificato se la finestra contenente il modulo adattivo è attiva. Se la finestra è attiva, viene attivato un `panelVisit`evento in Adobe  Analytics. È utile verificare che il documento o il modulo sia attivo e calcolare il tempo impiegato per il modulo o il documento corrispondente.

>[!NOTE]
>
>Il nome dell&#39;evento utilizzato per tenere traccia dell&#39;attività e calcolare il tempo trascorso è &quot;panelVisit&quot;. Questo evento è diverso dall’evento della visita del pannello elencato nella tabella precedente.

È possibile modificare la funzione ScheduleHeartBeatCheck disponibile nel `/libs/afanalytics/js/custom.js` file per modificare o interrompere l&#39;evento inviato ad Adobe  Analytics a intervalli regolari.
