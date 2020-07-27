---
title: Personalizzazione delle schede per un'attività
seo-title: Personalizzazione delle schede per un'attività
description: Procedura per personalizzare i nomi delle schede delle attività, nell'area di lavoro AEM Forms LiveCycle.
seo-description: Procedura per personalizzare i nomi delle schede delle attività, nell'area di lavoro AEM Forms LiveCycle.
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Personalizzazione delle schede per un&#39;attività {#customizing-tabs-for-a-task}

Potete personalizzare i nomi delle schede per il `Start Process` componente nella vista `Start Process` Uber e per il `Task Details` componente nella vista `ToDo` Uber.

1. Seguite la procedura [Generico per la personalizzazione](/help/forms/using/generic-steps-html-workspace-customization.md)dell’area di lavoro AEM Forms.
1. Modificate il valore di `tabname`nel `translation.json` file.

   Ad esempio, cambiare `/apps/ws/locales/en-US/translation.json` per Inglese nel modo seguente.

   * Per le attività iniziate nel processo di avvio, utilizzare il frammento seguente del `"startprocess" : {}` blocco.

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * Per le attività in Operazioni da eseguire, utilizzare il frammento seguente del `"todo" : {}` blocco.

   ```json
   "tabname" : {
               "summary" : "Bird's-eye view",
               "history" : "Past",
               "form" : "Form",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Notes"
   }
   ```

   >[!NOTE]
   >
   >Aggiungete la coppia chiave-valore corrispondente per tutte le lingue supportate.
