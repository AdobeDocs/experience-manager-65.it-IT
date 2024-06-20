---
title: Personalizzazione delle schede per un’attività
description: Come personalizzare i nomi delle schede per le attività, nell’area di lavoro di LiveCycle AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# Personalizzazione delle schede per un’attività {#customizing-tabs-for-a-task}

È possibile personalizzare i nomi delle schede per `Start Process` componente in `Start Process` Visualizzazione Uber e `Task Details` componente in `ToDo` Vista Uber.

1. Segui le [Passaggi generici per la personalizzazione dell’area di lavoro AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Modifica il valore di `tabname`nel `translation.json` file.

   Ad esempio, modifica `/apps/ws/locales/en-US/translation.json` per l’inglese, procedere come segue.

   * Per le attività avviate nel processo di avvio, utilizzare lo snippet seguente del `"startprocess" : {}` blocco.

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * Per le attività in Da fare, utilizza lo snippet seguente della `"todo" : {}` blocco.

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
