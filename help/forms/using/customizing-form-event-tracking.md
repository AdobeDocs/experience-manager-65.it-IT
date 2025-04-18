---
title: Personalizzazione del tracciamento degli eventi dei moduli
description: Se un utente trascorre più di 60 secondi su un campo, si attiva un evento fieldvisit e i dettagli del campo vengono inviati ad Adobe SiteCatalyst.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
exl-id: d0280a15-5d0d-49cf-bce9-ad1c40530eae
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 8a77756e8ba771c8de9950c2323bef8f23cc59b4
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---

# Personalizzazione del tracciamento degli eventi dei moduli {#customizing-form-event-tracking}

In un modulo adattivo abilitato per l’analisi vengono tracciati i seguenti eventi predefiniti:

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
   <td>invia</td>
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

## Personalizzazione del timeout dell’evento di visita in campo {#customizing-the-field-visit-event-timeout}

Nella configurazione predefinita del modulo AEM, se un utente trascorre più di 60 secondi su un campo, si attiva un evento `fieldvisit` e i dettagli del campo vengono inviati ad Adobe Analytics. Puoi personalizzare la linea di base del tracciamento temporale dei campi in Configurazione di AEM Forms Analytics nella console di configurazione AEM (/system/console/configMgr) per aumentare o ridurre il limite di timeout.

## Personalizzazione degli eventi di tracciamento {#customizing-the-tracking-events}

È possibile modificare la funzione `trackEvent` disponibile nel file `/libs/afanalytics/js/custom.js` per personalizzare il tracciamento degli eventi. Ogni volta che si verifica un evento monitorato in un modulo adattivo, viene chiamata la funzione `trackEvent`. La funzione `trackEvent` accetta due parametri: `eventName` e `variableValueMap`.

È possibile valutare il valore degli argomenti *eventName* e *variableValueMap* per modificare il comportamento di tracciamento degli eventi. Ad esempio, puoi scegliere di inviare le informazioni al server di Analytics dopo che si è verificato un certo numero di eventi di errore. È inoltre possibile scegliere di eseguire una delle seguenti personalizzazioni:

* Puoi impostare un tempo di soglia prima di inviare l’evento.
* Puoi mantenere uno stato per decidere l&#39;azione, ad esempio *fieldVisit* invia un evento fittizio in base alla marca temporale dell&#39;ultimo evento.
* È possibile utilizzare la funzione `pushEvent` per inviare l&#39;evento al server di analisi *.*

* Puoi scegliere di non inviare l’evento al server di Analytics.

### Esempio {#sample}

Nell&#39;esempio seguente viene mantenuto lo stato per l&#39;evento *error* di ogni attributo *fieldName*. L’evento viene inviato al server di analisi solo se si verifica di nuovo un errore.

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## Personalizzazione dell’evento panelvisit {#customizing-the-panelvisit-event}

Nella configurazione predefinita di AEM Forms, ogni 60 secondi viene verificato se la finestra contenente il modulo adattivo è attiva. Se la finestra è attiva, viene attivato un evento `panelVisit` in Adobe Analytics. Consente di verificare che il documento o il modulo sia attivo e di calcolare il tempo impiegato per il modulo o il documento corrispondente.

>[!NOTE]
>
>Il nome dell’evento utilizzato per verificare l’attività e calcolare il tempo trascorso è &quot;panelVisit&quot;. Questo evento è diverso dall’evento di visita del pannello elencato nella tabella precedente.

È possibile modificare la funzione scheduleHeartBeatCheck disponibile nel file `/libs/afanalytics/js/custom.js` per modificare o interrompere questo evento inviato ad Adobe Analytics a intervalli regolari.
