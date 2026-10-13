---
title: Personalizzazione delle schede per un’attività
description: Come personalizzare i nomi delle schede per le attività, nell’area di lavoro di AEM Forms LiveCycle.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 9%
---
# Personalizzazione delle schede per un’attività {#customizing-tabs-for-a-task}

È possibile personalizzare i nomi delle schede per il componente `Start Process` nella visualizzazione Uber `Start Process` e il componente `Task Details` nella visualizzazione Uber `ToDo`.

1. Segui i [passaggi generici per la personalizzazione dell&#39;area di lavoro di AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Modificare il valore di `tabname` nel file `translation.json`.

   Modificare ad esempio `/apps/ws/locales/en-US/translation.json` per l&#39;inglese nel modo seguente.

   * Per le attività avviate nel processo di avvio, utilizzare lo snippet seguente del blocco `"startprocess" : {}`.

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * Per le attività in Da fare, utilizzare lo snippet seguente del blocco `"todo" : {}`.

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
   >Aggiungi una coppia chiave-valore corrispondente per tutte le lingue supportate.
