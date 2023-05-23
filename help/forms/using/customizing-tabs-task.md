---
title: Personalizzazione delle schede per un’attività
seo-title: Customizing tabs for a task
description: Come personalizzare i nomi delle schede per le attività, nell’area di lavoro di LiveCycle AEM Forms.
seo-description: How-to customize the names of the tabs for your tasks, in LiveCycle AEM Forms workspace.
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
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
