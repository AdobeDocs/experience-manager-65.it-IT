---
title: Registrazione di una transazione per le implementazioni personalizzate
seo-title: Registrazione di una transazione per le implementazioni personalizzate
description: Utilizzare l'API TransactionRecorder per registrare automaticamente le azioni non contabilizzate come transazioni
seo-description: Utilizzare l'API TransactionRecorder per registrare automaticamente le azioni non contabilizzate come transazioni
uuid: a22b1a0b-7553-4a17-8fb4-a3bee97b4a98
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 0d961630-573b-4c8e-902f-996f1d1265b6
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Registra una transazione per implementazioni personalizzate {#record-a-transaction-for-custom-implementations}

Utilizzare l&#39;API TransactionRecorder per registrare automaticamente le azioni non contabilizzate come transazioni

È possibile utilizzare un codice personalizzato per inviare un modulo PDF, l&#39;URL di anteprima dell&#39;interfaccia utente agente agli utenti finali per visualizzare l&#39;anteprima di una comunicazione interattiva, oppure per inviare un modulo utilizzando metodi personalizzati invece di utilizzare i metodi di invio forniti con  AEM Forms. Tutte le azioni e le implementazioni personalizzate precedentemente citate  API AEM Forms non sono considerate transazioni.  AEM Forms fornisce un&#39;API, [TransactionRecorder](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html), per registrare azioni come le transazioni.

Per registrare una transazione, scrivere il [servlet sling standard](https://helpx.adobe.com/experience-manager/using/custom-sling-servlets.html) e chiamare il servlet da un client per registrare una transazione. È possibile chiamare il servlet utilizzando AJAX o qualsiasi altro metodo standard.

## Esempio di codice lato server {#sample-server-sided-code}

È possibile utilizzare il codice di esempio seguente per eseguire l&#39;API TransactionRecorder da una classe JAVA utilizzando un bundle OSGi personalizzato.

```java
import com.adobe.aem.transaction.core.ITransactionRecorder;
import com.adobe.aem.transaction.core.model.TransactionRecord;
import com.adobe.aem.transaction.core.exception.TransactionException;
import com.adobe.aem.transaction.core.FormsTransactionConstants;

@Reference
private ITransactionRecorder transactionRecorder;

doPost (SlingHttpServletRequest request, SlingHttpServletResponse response) {
    transactionRecorder.startContext();
    TransactionRecord txRecord = extractTxRecordFromRequest(request); //extract transaction relevant data from request
    try {
        bool success = doBillableWork();
        if (success) {
            transactionRecorder.recordTransaction(txRecord);
        }
    } catch (Exception e) {
        //exception handling
    } finally {
        transactionRecorder.endContext();
    }
}

//Here, it is assumed that txInfo is passed in Stringified json form in the ajax call (in data parameter). You can pass txInfo from client in any way that you find suitable.
private TransactionRecord extractTxRecordFromRequest(SlingHttpServletRequest request) {
    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(request.getInputStream()));
    Map<String, Object> txDataMap = new HashMap<String, Object>();
    String txData = bufferedReader.readLine();
    JSONObject txInfo= new JSONObject(txData );
    try {
        String resourceType= txInfo.getString("resourceType");
        String transactionType = txInfo.getString("transactionType");
        Integer transactionCount = (Integer)txInfo.get("transactionCount");
        //Extract all the relevant tx record attributes similarly and pass them in Transaction Record constructor as per the java doc}
        return new TransactionRecord(transactionCount, transactionType, resourceType, ..);
    } catch (JSONException e) {
        //exception handling
    } finally {
        bufferedReader.close();
    }
}
```

## Esempio di codice lato client {#sample-client-side-code}

Potete utilizzare il codice di esempio riportato di seguito per chiamare il servlet che dispone dell&#39;API `TransactionRecorder`.

```javascript
$.ajax({
   type: 'POST',
   url: url, //servlet url
   contentType: 'application/json; UTF-8',
   data: JSON.stringify({transactionCount : 1,
                        transactionType: "SUBMIT",
                        resourceType: "FORM",
                        resourceSubType: "ADAPTIVE-FORM"}),
   success: successHandler,
   error: faultHandler
})
```

## Articoli correlati {#related-articles}

* [Panoramica dei report sulle transazioni](/help/forms/using/transaction-reports-overview.md)
* [Visualizzazione e comprensione di rapporti sulle transazioni](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [API fatturabili report transazioni](/help/forms/using/transaction-reports-billable-apis.md)

