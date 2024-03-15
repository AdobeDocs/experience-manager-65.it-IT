---
title: Registra una transazione per l’API del componente personalizzato per AEM Forms su JEE.
description: Utilizza l’API TransactionRecorder per registrare la transazione per il componente personalizzato.
feature: Transaction Reports
source-git-commit: d0db00de6b767a12a9492bbbcec49a8c5d25ff27
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# Registrare una transazione per le API dei componenti personalizzati per AEM Forms su JEE {#record-a-transaction-for-custom-components}

Quando utilizzi le API fatturabili nel componente personalizzato, puoi abilitare il reporting delle transazioni per il componente. Per abilitare la generazione di rapporti sulle transazioni, modificare la `component.xml` del componente e aggiungi il tag indicato di seguito nell’operazione per la quale deve essere abilitata la generazione rapporti sulle transazioni.

**Tag**: `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| Tag precedente dell’operazione | Nuovo tag operazione |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

Se è necessario acquisire più di una transazione per un’API, ad esempio, nel caso di un’API batch in cui il conteggio delle transazioni può variare in base al numero di conteggi di input, in questi casi è necessario gestire il conteggio delle transazioni a livello di API. Di seguito sono riportati i passaggi forniti per registrare il conteggio delle transazioni variabili:

1. Importa classe `"com.adobe.idp.dsc.InvocationContextStack"` nel codice. La classe fa parte della classe `adobe-livecycle-client.jar` file sdk. Il file sdk è disponibile all’indirizzo `<AEM_Forms_JEE_Install>\sdk\client-libs\common`

   >[!NOTE]
   > Aggiorna il file client condiviso in precedenza nel progetto client con il nuovo file, se è già incluso nel bundle.

1. Nell’API per la quale è necessario registrare le transazioni varie:
   1. Aggiungi una logica per memorizzare il conteggio delle transazioni in alcune variabili intere, ad esempio: `transaction_count`.
   1. Quando l’operazione ha esito positivo, aggiungi `InvocationContextStack.recordTransactionCount(transaction_count)`.

<!--For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.-->

## Articoli correlati

* [Abilitazione e visualizzazione del rapporto sulle transazioni per AEM Forms su JEE](/help/forms/using/transaction-report-overview-jee.md)
* [Elenco delle API fatturabili per AEM Forms su JEE](/help/forms/using/transaction-reports-billable-apis-jee.md)


