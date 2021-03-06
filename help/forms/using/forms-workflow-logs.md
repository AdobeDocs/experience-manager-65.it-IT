---
title: Accesso  flussi di lavoro AEM Forms
seo-title: Accesso  flussi di lavoro AEM Forms
description: Utilizzate i registri per eseguire il debug  problemi del flusso di lavoro AEM Forms.
seo-description: Utilizzate i registri per eseguire il debug  problemi del flusso di lavoro AEM Forms.
uuid: 869d0271-c7e3-4b6d-8e63-893dc6af8b8a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 14bb521a-42ea-4fe2-90fb-202e7ddf917a
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 5%

---


# Accesso  flussi di lavoro AEM Forms{#logging-in-aem-forms-workflows}

I passaggi del flusso di lavoro Forms forniscono registri dettagliati per il debug dei problemi relativi ai flussi di lavoro in modo conveniente. Abilita la registrazione di debug per  flussi di lavoro AEM Forms per visualizzare i registri.

Per impostazione predefinita, tutte le informazioni di registrazione sono disponibili nel file **error.log** nella directory */crx-repository/logs/*.

I registri di debug per i flussi di lavoro dei moduli includono:

* Immissione di ogni passaggio del flusso di lavoro. Esempio:\
   `[DEBUG] "Executing Invoke DDX Process step"`

* Esci da ogni passaggio del flusso di lavoro. Esempio:\
   `[DEBUG] "Successfully finished Invoke DDX Process step"`

* Messaggi di chiamata del servizio. Esempio:\
   `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* Messaggi di uscita dal servizio. Esempio:\
   `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* Variabili lette dalla mappa di metadati. Esempio:\
   `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* Variabili scritte nell&#39;archivio JCR. Esempio:

   ```verilog
      [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
   ```

* Messaggi di eccezione con traccia dello stack completa. Esempio:\
   `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* Parametri di metadati dei passaggi dinamici. Esempio:

   ```verilog
   [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
    [DEBUG] Locale to be used for Document of Record is <locale>
   ```

L&#39;esempio seguente illustra i registri relativi al passaggio Firma documento:

```verilog
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

Utilizzate i registri per valutare che:

* Stai utilizzando una configurazione Adobe Sign corretta.
* Il servizio Adobe Sign  si chiude dopo la creazione di un accordo.
* Il passaggio Firma documento esce con un messaggio di riuscita.

In caso di eccezione, ?? possibile visualizzare l&#39;analisi completa dello stack per valutare la causa dell&#39;errore.

## Abilita registrazione di debug per  flussi di lavoro AEM Forms {#enable-debug-logging-for-aem-forms-workflows}

Per attivare la registrazione di debug per  flussi di lavoro AEM Forms, effettuate le seguenti operazioni:

1. AEM gestione della configurazione della console Web all&#39;indirizzo:

   https://&#39;[server]:[porta]&#39;/system/console/configMgr

1. Selezionare **[!UICONTROL Sling]** > **[!UICONTROL Log Support]**.
1. Toccate **[!UICONTROL Aggiungi nuovo registro.]**
1. Selezionare **[!UICONTROL Debug]** come **[!UICONTROL Livello di registro]**.
1. Specificate il percorso del file di registro. Il percorso predefinito per il file di registro ??: *log\error.log*
1. Specificate il nome del pacchetto come **com.adobe.granite.workflow.core** nella colonna **[!UICONTROL Logger]**.

   L&#39;esecuzione di questi passaggi consente di memorizzare i registri di debug per il pacchetto **com.adobe.granite.workflow.core**. Toccate **[!UICONTROL +]** e aggiungete i seguenti nomi di pacchetto all&#39;elenco:

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace

