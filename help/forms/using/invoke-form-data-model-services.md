---
title: API per richiamare il servizio del modello dati modulo dai moduli adattivi
seo-title: API to invoke form data model service from adaptive forms
description: Spiega l’API invokeWebServices che è possibile utilizzare per richiamare servizi Web scritti in WSDL da un campo modulo adattivo.
seo-description: Explains the invokeWebServices API that you can use to invoke web services written in WSDL from within an adaptive form field.
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: Adaptive Forms
exl-id: cf037174-3153-486f-85b1-c974cd5a1ace
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# API per richiamare il servizio del modello dati modulo dai moduli adattivi {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## Panoramica {#overview}

AEM Forms consente agli autori dei moduli di semplificare e migliorare ulteriormente l’esperienza di compilazione dei moduli richiamando i servizi configurati in un modello di dati del modulo dall’interno di un campo modulo adattivo. Per richiamare un servizio del modello dati, puoi creare una regola nell’editor visivo o specificare un JavaScript utilizzando `guidelib.dataIntegrationUtils.executeOperation` API nell’editor di codice del [editor di regole](/help/forms/using/rule-editor.md).

Questo documento si concentra sulla scrittura di un JavaScript utilizzando `guidelib.dataIntegrationUtils.executeOperation` API per richiamare un servizio.

## Utilizzo dell’API {#using-the-api}

La `guidelib.dataIntegrationUtils.executeOperation` L’API richiama un servizio dall’interno di un campo modulo adattivo. La sintassi API è la seguente:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

La struttura del `guidelib.dataIntegrationUtils.executeOperation` API specifica i dettagli sull&#39;operazione del servizio. La sintassi della struttura è la seguente.

```javascript
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

La struttura API specifica i seguenti dettagli sull’operazione del servizio.

<table>
 <tbody>
  <tr>
   <th>Parametro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>Struttura per specificare l’identificatore del modello di dati del modulo, il titolo dell’operazione e il nome dell’operazione</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>Specifica il percorso del repository del modello dati del modulo, incluso il suo nome</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>Specifica il nome dell'operazione del servizio da eseguire</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>Mappa uno o più oggetti modulo agli argomenti di input per l'operazione del servizio</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>Mappa uno o più oggetti modulo ai valori di output dall’operazione del servizio per comporre i campi modulo<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>Restituisce valori in base agli argomenti di input per l'operazione del servizio. Si tratta di un parametro facoltativo utilizzato come funzione di callback.<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>Visualizza un messaggio di errore se la funzione di callback di successo non riesce a visualizzare i valori di output in base agli argomenti di input. Si tratta di un parametro facoltativo utilizzato come funzione di callback.<br /> </td>
  </tr>
 </tbody>
</table>

## Script di esempio per richiamare un servizio {#sample-script-to-invoke-a-service}

Lo script di esempio seguente utilizza `guidelib.dataIntegrationUtils.executeOperation` API per richiamare `getAccountById` operazione di servizio configurata in `employeeAccount` modello dati modulo.

La `getAccountById` prende il valore nel `employeeID` campo modulo come input per `empId` argomento e restituisce il nome del dipendente, il numero di conto e il saldo del conto per il dipendente corrispondente. I valori di output vengono compilati nei campi modulo specificati. Ad esempio, il valore in `name` viene popolato in `fullName` elemento e valore modulo per `accountNumber` argomento in `account` elemento modulo.

```javascript
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

## Utilizzo dell&#39;API con la funzione di callback {#using-the-api-callback}

È inoltre possibile richiamare il servizio del modello dati modulo utilizzando `guidelib.dataIntegrationUtils.executeOperation` API con una funzione di callback. La sintassi API è la seguente:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

La funzione di chiamata di ritorno può avere `success` e `failure` funzioni di callback.

### Script di esempio con funzioni di callback di successo e di errore {#callback-function-success-failure}

Lo script di esempio seguente utilizza `guidelib.dataIntegrationUtils.executeOperation` API per richiamare `GETOrder` operazione di servizio configurata in `employeeOrder` modello dati modulo.

La `GETOrder` prende il valore nel `Order ID` campo modulo come input per `orderId` argomento e restituisce il valore della quantità dell&#39;ordine nel `success` funzione di callback.  Se la `success` la funzione di callback non restituisce la quantità dell&#39;ordine, il `failure` la funzione di callback visualizza `Error occured` messaggio.

>[!NOTE]
>
> Se utilizzi `success` funzione di callback, i valori di output non vengono compilati nei campi modulo specificati.

```javascript
var operationInfo = {
    "formDataModelId": "/content/dam/formsanddocuments-fdm/employeeOrder",
    "operationTitle": "GETOrder",
    "operationName": "GETOrder"
};
var inputs = {
    "orderId" : Order ID
};
var outputs = {};
var success = function (wsdlOutput, textStatus, jqXHR) {
order_quantity.value = JSON.parse(wsdlOutput).quantity;
 };
var failure = function(){
alert('Error occured');
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, success, failure);
```
