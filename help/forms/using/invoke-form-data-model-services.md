---
title: API per richiamare il servizio del modello dati modulo dai moduli adattivi
seo-title: API per richiamare il servizio del modello dati modulo dai moduli adattivi
description: Spiega l'API invokeWebServices che è possibile utilizzare per richiamare i servizi Web scritti in WSDL da un campo modulo adattivo.
seo-description: Spiega l'API invokeWebServices che è possibile utilizzare per richiamare i servizi Web scritti in WSDL da un campo modulo adattivo.
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# API per richiamare il servizio del modello dati modulo dai moduli adattivi {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## Panoramica {#overview}

AEM Forms consente agli autori dei moduli di semplificare e migliorare ulteriormente l&#39;esperienza di compilazione richiamando i servizi configurati in un modello dati modulo da un campo modulo adattivo. Per richiamare un servizio del modello dati, è possibile creare una regola nell&#39;editor visivo o specificare un JavaScript utilizzando l&#39; `guidelib.dataIntegrationUtils.executeOperation` API nell&#39;editor di codice dell&#39;editor [di](/help/forms/using/rule-editor.md)regole.

Questo documento è incentrato sulla scrittura di JavaScript tramite l&#39; `guidelib.dataIntegrationUtils.executeOperation` API per richiamare un servizio.

## Utilizzo dell&#39;API {#using-the-api}

L&#39; `guidelib.dataIntegrationUtils.executeOperation` API richiama un servizio dall&#39;interno di un campo modulo adattivo. La sintassi API è la seguente:

```
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

L&#39;API richiede i seguenti parametri.

| Parametro | Descrizione |
|---|---|
| `operationInfo` | Struttura per specificare l&#39;identificatore del modello dati del modulo, il titolo dell&#39;operazione e il nome dell&#39;operazione |
| `inputs` | Struttura per specificare gli oggetti modulo i cui valori vengono immessi nell&#39;operazione del servizio |
| `outputs` | Struttura per specificare gli oggetti modulo che verranno compilati con i valori restituiti dall&#39;operazione del servizio |

La struttura dell&#39; `guidelib.dataIntegrationUtils.executeOperation` API specifica i dettagli sull&#39;operazione del servizio. La sintassi della struttura è la seguente.

```
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

La struttura API specifica i seguenti dettagli sull&#39;operazione del servizio.

<table>
 <tbody>
  <tr>
   <th>Parametro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>forDataModelId</code></td>
   <td>Specificare il percorso dell'archivio del modello dati del modulo con il relativo nome</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>Specificare il nome dell'operazione del servizio da eseguire</td>
  </tr>
  <tr>
   <td><code>input</code></td>
   <td>Mappare uno o più oggetti modulo agli argomenti di input per l'operazione del servizio</td>
  </tr>
  <tr>
   <td>Output</td>
   <td>Mappare uno o più oggetti modulo ai valori di output dall'operazione del servizio per compilare i campi del modulo<br /> </td>
  </tr>
 </tbody>
</table>

## Script di esempio per richiamare un servizio {#sample-script-to-invoke-a-service}

Lo script di esempio seguente utilizza l&#39; `guidelib.dataIntegrationUtils.executeOperation` API per richiamare l&#39;operazione di `getAccountById` servizio configurata nel modello dati del `employeeAccount` modulo.

L&#39; `getAccountById` operazione prende il valore nel campo `employeeID` modulo come input per l&#39; `empId` argomento e restituisce il nome del dipendente, il numero del conto e il saldo del conto per il dipendente corrispondente. I valori di output vengono compilati nei campi modulo specificati. Ad esempio, il valore nell&#39; `name` argomento è popolato nell&#39;elemento `fullName` modulo e il valore per l&#39; `accountNumber` argomento nell&#39;elemento `account` modulo.

```
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

