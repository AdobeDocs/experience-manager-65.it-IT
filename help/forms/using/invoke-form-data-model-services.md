---
title: API per richiamare il servizio del modello dati modulo dai moduli adattivi
seo-title: API per richiamare il servizio del modello dati modulo dai moduli adattivi
description: Spiega l’API invokeWebServices che è possibile utilizzare per richiamare servizi Web scritti in WSDL da un campo modulo adattivo.
seo-description: Spiega l’API invokeWebServices che è possibile utilizzare per richiamare servizi Web scritti in WSDL da un campo modulo adattivo.
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: Moduli adattivi
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# API per richiamare il servizio del modello dati modulo dai moduli adattivi {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## Panoramica {#overview}

AEM Forms consente agli autori dei moduli di semplificare e migliorare ulteriormente l’esperienza di compilazione dei moduli richiamando i servizi configurati in un modello di dati del modulo dall’interno di un campo modulo adattivo. Per richiamare un servizio del modello dati, puoi creare una regola nell’editor visivo o specificare un JavaScript utilizzando l’ `guidelib.dataIntegrationUtils.executeOperation` API nell’editor di codice dell’ [editor di regole](/help/forms/using/rule-editor.md).

Questo documento si concentra sulla scrittura di un JavaScript utilizzando l’ `guidelib.dataIntegrationUtils.executeOperation` API per richiamare un servizio.

## Utilizzo dell&#39;API {#using-the-api}

L’ API `guidelib.dataIntegrationUtils.executeOperation` richiama un servizio dall’interno di un campo modulo adattivo. La sintassi API è la seguente:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

La struttura dell’ API `guidelib.dataIntegrationUtils.executeOperation` specifica i dettagli sull’operazione del servizio. La sintassi della struttura è la seguente.

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
   <td>Mappa uno o più oggetti modulo ai valori di output dall'operazione del servizio per comporre i campi modulo<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>Restituisce valori in base agli argomenti di input per l'operazione del servizio. Si tratta di un parametro opzionale utilizzato come funzione di callback.<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>Visualizza un messaggio di errore se la funzione di callback di successo non riesce a visualizzare i valori di output in base agli argomenti di input. Si tratta di un parametro opzionale utilizzato come funzione di callback.<br /> </td>
  </tr>
 </tbody>
</table>

## Script di esempio per richiamare un servizio {#sample-script-to-invoke-a-service}

Lo script di esempio seguente utilizza l&#39;API `guidelib.dataIntegrationUtils.executeOperation` per richiamare l&#39;operazione del servizio `getAccountById` configurata nel modello di dati del modulo `employeeAccount`.

L&#39;operazione `getAccountById` considera il valore nel campo modulo `employeeID` come input per l&#39;argomento `empId` e restituisce il nome del dipendente, il numero di conto e il saldo del conto del dipendente corrispondente. I valori di output vengono compilati nei campi modulo specificati. Ad esempio, il valore nell’argomento `name` viene popolato nell’elemento e nel valore `fullName` del modulo `accountNumber` per l’argomento  nell’elemento modulo `account`.

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

È inoltre possibile richiamare il servizio del modello dati del modulo utilizzando l’ API `guidelib.dataIntegrationUtils.executeOperation` con una funzione di callback. La sintassi API è la seguente:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

La funzione di chiamata di ritorno può avere le funzioni di callback `success` e `failure` .

### Script di esempio con funzioni di callback di successo e non riuscite {#callback-function-success-failure}

Lo script di esempio seguente utilizza l&#39;API `guidelib.dataIntegrationUtils.executeOperation` per richiamare l&#39;operazione del servizio `GETOrder` configurata nel modello di dati del modulo `employeeOrder`.

L&#39;operazione `GETOrder` prende il valore nel campo modulo `Order ID` come input per l&#39;argomento `orderId` e restituisce il valore della quantità dell&#39;ordine nella funzione di callback `success`.  Se la funzione di callback `success` non restituisce la quantità dell&#39;ordine, la funzione di callback `failure` visualizza il messaggio `Error occured`.

>[!NOTE]
>
> Se si utilizza la funzione di callback `success`, i valori di output non vengono compilati nei campi del modulo specificati.

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
