---
title: Personalizzazione delle schede per un'attività
seo-title: Personalizzazione delle schede per un'attività
description: Come personalizzare i nomi delle schede per le attività, nell'area di lavoro  LiveCycle di AEM Forms.
seo-description: Come personalizzare i nomi delle schede per le attività, nell'area di lavoro  LiveCycle di AEM Forms.
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

È possibile personalizzare i nomi delle schede per il componente `Start Process` nella `Start Process` Uber view e per il componente `Task Details` nella `ToDo` Uber view.

1. Seguite i passaggi [Generici per  personalizzazione dell&#39;area di lavoro AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Modificare il valore di `tabname`nel file `translation.json`.

   Ad esempio, modificare `/apps/ws/locales/en-US/translation.json` per l&#39;inglese nel modo seguente.

   * Per le attività iniziate nel processo di avvio, utilizzare il frammento seguente dal blocco `"startprocess" : {}`.

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * Per le attività in Operazioni da eseguire, utilizzare il frammento seguente del blocco `"todo" : {}`.

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
