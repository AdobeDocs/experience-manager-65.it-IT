---
title: Personalizzazione delle schede per un'attività
seo-title: Personalizzazione delle schede per un'attività
description: Come personalizzare i nomi delle schede delle attività nell'area di lavoro LiveCycle AEM Forms.
seo-description: Come personalizzare i nomi delle schede delle attività nell'area di lavoro LiveCycle AEM Forms.
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Personalizzazione delle schede per un&#39;attività {#customizing-tabs-for-a-task}

Potete personalizzare i nomi delle schede per il `Start Process` componente nella vista `Start Process` Uber e per il `Task Details` componente nella vista `ToDo` Uber.

1. Seguite i passaggi [Generici per la personalizzazione](/help/forms/using/generic-steps-html-workspace-customization.md)dell&#39;area di lavoro AEM Forms.
1. Modificate il valore di `tabname`nel `translation.json` file.

   Ad esempio, cambiare `/apps/ws/locales/en-US/translation.json` per Inglese nel modo seguente.

   * Per le attività avviate nel processo di avvio, utilizzare il frammento seguente del `"startprocess" : {}` blocco.

   ```
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * Per le attività in Operazioni da eseguire, utilizzare il frammento seguente del `"todo" : {}` blocco.

   ```
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

[Contattare il supporto](https://www.adobe.com/account/sign-in.supportportal.html)
