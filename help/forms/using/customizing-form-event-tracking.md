---
title: Personalizzazione del tracciamento degli eventi modulo
seo-title: Personalizzazione del tracciamento degli eventi modulo
description: Se un utente trascorre più di 60 secondi su un campo, viene attivato un evento field visit e i dettagli del campo vengono inviati a  Adobe SiteCatalyst.
seo-description: Se un utente trascorre più di 60 secondi su un campo, viene attivato un evento field visit e i dettagli del campo vengono inviati a  Adobe SiteCatalyst.
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


# Personalizzazione del tracciamento eventi modulo {#customizing-form-event-tracking}

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

## Personalizzazione del timeout dell&#39;evento visita del campo {#customizing-the-field-visit-event-timeout}

Nell&#39;impostazione predefinita AEM modulo, se un utente spende più di 60 secondi su un campo, viene attivato un evento `fieldvisit` e i dettagli del campo vengono inviati a  Adobe Analytics. Puoi personalizzare la linea di base per il tracciamento dell’ora del campo in  configurazione di AEM Forms Analytics AEM console di configurazione (/system/console/configMgr) per aumentare o diminuire il limite di timeout.

## Personalizzazione degli eventi di tracciamento {#customizing-the-tracking-events}

È possibile modificare la funzione `trackEvent`disponibile nel file `/libs/afanalytics/js/custom.js` per personalizzare il tracciamento dell&#39;evento. Ogni volta che si verifica un evento in corso di tracciamento in un modulo adattivo, viene chiamata la funzione `trackEvent`. La funzione `trackEvent` accetta due parametri: `eventName`e `variableValueMap`.

È possibile valutare il valore degli argomenti *eventName* e *variableValueMap* per modificare il comportamento di tracciamento degli eventi. Ad esempio, potete scegliere di inviare le informazioni al server di analisi dopo un certo numero di eventi di errore. Potete anche scegliere di eseguire una delle seguenti personalizzazioni:

* Potete impostare un&#39;ora di soglia prima di inviare l&#39;evento.
* È possibile mantenere uno stato per decidere l&#39;azione, ad esempio *fieldVisit* invia un evento fittizio in base alla marca temporale dell&#39;ultimo evento.
* È possibile utilizzare la funzione `pushEvent` per inviare l&#39;evento al server di analisi *.*

* Potete scegliere di non inviare l&#39;evento al server di analisi.

### Esempi {#sample}

Nell&#39;esempio seguente, viene mantenuto lo stato per l&#39;evento *error* di ciascun attributo *fieldName*. L&#39;evento viene inviato al server di analisi solo se si verifica di nuovo un errore.

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## Personalizzazione dell&#39;evento panelvisit {#customizing-the-panelvisit-event}

Per impostazione predefinita  AEM Forms, dopo 60 secondi viene verificato se la finestra contenente il modulo adattivo è attiva. Se la finestra è attiva, viene attivato un evento `panelVisit` Adobe Analytics. È utile verificare che il documento o il modulo sia attivo e calcolare il tempo impiegato per il modulo o il documento corrispondente.

>[!NOTE]
>
>Il nome dell&#39;evento utilizzato per tenere traccia dell&#39;attività e calcolare il tempo trascorso è &quot;panelVisit&quot;. Questo evento è diverso dall’evento della visita del pannello elencato nella tabella precedente.

È possibile modificare la funzione ScheduleHeartBeatCheck disponibile nel file `/libs/afanalytics/js/custom.js` per modificare o interrompere l&#39;evento inviato a  Adobe Analytics a intervalli regolari.
