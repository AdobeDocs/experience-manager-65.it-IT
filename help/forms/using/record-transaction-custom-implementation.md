---
title: Registrare una transazione per le implementazioni personalizzate
description: Utilizzare l'API TransactionRecorder per registrare automaticamente le azioni che non vengono contabilizzate come transazioni.
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
feature: Transaction Reports
exl-id: b0c4f72a-e65f-453a-af66-5d9f98a9d6df
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: bcb3e79d-a57e-59a4-ad50-e03803c9f153
    internal-label: Transaction Reports
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 7%
---
# Registrare una transazione per le implementazioni personalizzate per AEM Forms su OSGi {#record-a-transaction-for-custom-implementations}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/record-transaction-custom-implementation) |
| AEM 6.5 | Questo articolo |

Utilizzare l&#39;API TransactionRecorder per registrare automaticamente le azioni non contabilizzate come transazioni

Puoi utilizzare un codice personalizzato per inviare un PDF Form o per inviare agli utenti finali un URL di anteprima dell’interfaccia utente dell’agente per visualizzare un’anteprima di una comunicazione interattiva. In alternativa, è possibile inviare un modulo utilizzando metodi personalizzati anziché i metodi di invio forniti con AEM Forms. Tutte le azioni e le implementazioni personalizzate precedentemente menzionate delle API di AEM Forms non vengono contabilizzate come transazioni. AEM Forms fornisce un&#39;API, [TransactionRecorder](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html), per registrare azioni quali le transazioni.

Per registrare una transazione, scrivi il [servlet sling standard](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/store-and-retrieve-af-with-2fa/create-servlet.html?lang=it) e chiama il servlet da un client per registrare una transazione. Puoi chiamare il servlet utilizzando AJAX o qualsiasi altro metodo standard.

## Esempio di codice lato server {#sample-server-sided-code}

Puoi utilizzare il codice di esempio seguente per eseguire l’API TransactionRecorder da una classe Java™ utilizzando un bundle OSGi personalizzato.

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

È possibile utilizzare il codice di esempio seguente per chiamare il servlet che dispone dell&#39;API `TransactionRecorder`.

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

* [Panoramica dei rapporti sulle transazioni per AEM Forms su OSGi](/help/forms/using/transaction-reports-overview.md)
* [Visualizzazione e comprensione dei rapporti sulle transazioni per AEM Forms su OSGi](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [Rapporti sulle transazioni API fatturabili per AEM Forms su OSGi](/help/forms/using/transaction-reports-billable-apis.md)
