---
title: Registrazione nei flussi di lavoro di AEM Forms
seo-title: Logging in AEM Forms workflows
description: Utilizza i registri per eseguire il debug dei problemi del flusso di lavoro di AEM Forms.
seo-description: Use logs to debug AEM Forms workflow issues.
uuid: 869d0271-c7e3-4b6d-8e63-893dc6af8b8a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 14bb521a-42ea-4fe2-90fb-202e7ddf917a
docset: aem65
exl-id: 601c8d95-0d1a-4945-a522-e85d3e9fc4ae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 5%

---

# Registrazione nei flussi di lavoro di AEM Forms{#logging-in-aem-forms-workflows}

I passaggi del flusso di lavoro Forms forniscono registri dettagliati per eseguire il debug dei problemi correlati al flusso di lavoro in modo semplice. Abilita la registrazione di debug per i flussi di lavoro di AEM Forms per visualizzare i registri.

Per impostazione predefinita, tutte le informazioni di registrazione sono disponibili nel **error.log** file in corrispondenza di */crx-repository/logs/* directory.

I registri di debug per i flussi di lavoro dei moduli includono:

* Voce di ogni passaggio del flusso di lavoro. Ad esempio:\
   `[DEBUG] "Executing Invoke DDX Process step"`

* Uscita da ogni passaggio del flusso di lavoro. Ad esempio:\
   `[DEBUG] "Successfully finished Invoke DDX Process step"`

* Messaggi di chiamata al servizio. Ad esempio:\
   `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* Messaggi di uscita dal servizio. Ad esempio:\
   `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* Variabili lette dalla mappa dei metadati. Ad esempio:\
   `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* Variabili scritte nell’archivio JCR. Ad esempio:

   ```verilog
      [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
   ```

* Messaggi di eccezione con traccia dello stack completa. Ad esempio:\
   `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* Parametri dei metadati del passaggio dinamico. Ad esempio:

   ```verilog
   [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
    [DEBUG] Locale to be used for Document of Record is <locale>
   ```

L’esempio seguente illustra i registri per il passaggio Firma documento:

```verilog
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

Utilizza i registri per valutare quanto segue:

* Stai utilizzando una configurazione di Adobe Sign corretta.
* Il servizio Adobe Sign termina dopo la creazione di un contratto.
* Il passaggio Firma documento termina con un messaggio di successo.

In caso di eccezione, è possibile visualizzare l&#39;analisi completa dello stack per valutare la causa dell&#39;errore.

## Abilitare la registrazione di debug per i flussi di lavoro di AEM Forms {#enable-debug-logging-for-aem-forms-workflows}

Per abilitare la registrazione di debug per i flussi di lavoro AEM Forms, effettua le seguenti operazioni:

1. Vai a Gestione configurazione console web AEM all’indirizzo:

   https://&#39;[server]:[porta]&#39;/system/console/configMgr

1. Seleziona **[!UICONTROL Sling]** > **[!UICONTROL Supporto registro]**.
1. Tocca **[!UICONTROL Aggiungi nuovo logger.]**
1. Seleziona **[!UICONTROL Debug]** come **[!UICONTROL Livello registro]**.
1. Specificare il percorso del file di registro. Il percorso predefinito del file di registro è: *logs\error.log*
1. Specifica il nome del pacchetto come **com.adobe.granite.workflow.core** nel **[!UICONTROL Logger]** colonna.

   L’esecuzione di questi passaggi abilita l’archiviazione dei registri di debug per **com.adobe.granite.workflow.core** pacchetto. Tocca **[!UICONTROL +]** e aggiungi i seguenti nomi di pacchetto all’elenco:

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace
