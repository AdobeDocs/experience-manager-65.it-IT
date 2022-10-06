---
title: Visualizzazione di dati aggiuntivi nell'elenco ToDo
seo-title: Displaying additional data in ToDo list
description: Come personalizzare la visualizzazione dell’elenco A-fare dell’area di lavoro di LiveCycle AEM Forms per visualizzare ulteriori informazioni oltre a quelle predefinite.
seo-description: How-to customize the display of the To-do list of LiveCycle AEM Forms workspace to show more information besides the default.
uuid: 9467c655-dce2-43ce-8e8f-54542fe81279
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: fed3b562-bcc2-4fb7-8fd2-35b1ac621e16
docset: aem65
exl-id: f8b84f13-02d3-4787-95e1-25fd684e6d3b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 1%

---

# Visualizzazione di dati aggiuntivi nell&#39;elenco ToDo{#displaying-additional-data-in-todo-list}

Per impostazione predefinita, nell’elenco To-do dell’area di lavoro di AEM Forms vengono visualizzati il nome e la descrizione dell’attività. Tuttavia, puoi aggiungere altre informazioni, ad esempio data di creazione e data di scadenza. È inoltre possibile aggiungere icone e modificare lo stile della visualizzazione.

![Osserva la scheda To-do di HTML Workspace che mostra la configurazione predefinita](assets/html-todo-list.png)

Questo articolo descrive i passaggi per aggiungere informazioni da visualizzare per ogni attività nell&#39;elenco ToDo.

## Cosa può essere aggiunto {#what-can-be-added}

Puoi aggiungere le informazioni disponibili in `task.json` inviato dal server. Le informazioni possono essere aggiunte come testo normale oppure è possibile utilizzare gli stili per formattare le informazioni.

Per ulteriori informazioni sulla descrizione dell’oggetto JSON, consulta [questo](/help/forms/using/html-workspace-json-object-description.md) articolo.

## Visualizzazione di informazioni su un&#39;attività {#displaying-information-on-a-task}

1. Segui [Passaggi generici per la personalizzazione dell’area di lavoro AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md).
1. Per visualizzare informazioni aggiuntive per un&#39;attività, è necessario aggiungere le coppie chiave-valore corrispondenti all&#39;interno del blocco attività di `translation.json`.

   Esempio di modifica `/apps/ws/locales/en-US/translation.json` per inglese:

   ```json
   "task" : {
           "reminder" : {
               "value" : "Reminder",
               "tooltip" : "This is reminder __reminderCount__, for this task."
           },
           "deadlined" : {
               "value" : "Deadlined",
               "tooltip" : "This task has deadlined"
           },
           "save" : {
               "message" : "Task has been saved successfully"
           },
           "status" : {
               "deadlined" : "Deadlined",
               "created" : "Created",
               "assignedsaved" : "Draft from assigned task",
               "terminated" : "Terminated",
               "assigned" : "Assigned",
               "unknown" : "Unknown",
               "createdsaved" : "Draft from created task",
               "completed" : "Completed"
           },
           "draft" : {
               "value" : "Saved",
               "tooltip" : "This task is marked as a draft"
           },
           "escalated" : {
               "value" : "Escalated",
               "tooltip" : "This task has been escalated"
           },
           "forward" : {
               "value" : "Forwarded",
               "tooltip" : "This task was forwarded"
           },
           "priority" : {
               "highest" : "Highest priority",
               "normal" : "Normal priority",
               "high" : "High priority",
               "low" : "Low priority",
               "lowest" : "Lowest priority"
           },
           "claimed" : {
               "value" : "Claimed",
               "tooltip" : "This task has been claimed"
           },
           "locked" : {
               "value" : "Locked",
               "tooltip" : "This task is locked"
           },
           "consulted" : {
               "value" : "Consulted",
               "tooltip" : "This task has been consulted"
           },
           "returned" : {
               "value" : "Returned",
               "tooltip" : "This task was returned back"
           },
           "multiplesubmitbuttons" : {
               "message" : "The form associated with this task has multiple submit buttons so the Workspace Complete button will be disabled. Click the appropriate button on the form to submit it."
           },
           "nosubmitbutton" : {
               "message" : "The form associated with this task does not appear to have submit buttons. You may need to upgrade your Adobe Reader version to 9.1 or greater and enable the Reader Submit option in your process."
           },
           "icon" : {
               "tooltip" : "open the task __taskName__"
           }
       }
   ```

   >[!NOTE]
   >
   >Aggiungi le coppie chiave-valore corrispondenti per tutte le lingue supportate.

1. Ad esempio, aggiungere informazioni all’interno del blocco attività:

   ```json
   "stepname" : {
               "value" : "Step Name",
               "tooltip" : "This task belongs to __stepName__ step"
   }
   ```

## Definizione del CSS per la nuova proprietà {#defining-css-for-the-new-property}

1. È possibile applicare uno stile alle informazioni (proprietà) aggiunte a un&#39;attività. A questo scopo, è necessario aggiungere informazioni sugli stili per la nuova proprietà aggiunta a `/apps/ws/css/newStyle.css`.

   Ad esempio, aggiungi:

   ```css
   .task .taskProperties .stepname{
       width: 25px;
       background: url(../images/stepname.png) no-repeat; /*-------- Or just reuse background image / image-sprite defined .task .taskProperties span of style.css---------------------*/
       background-position: 0px 0px; /*-------- Dummy values, need to be configured as per user background image / image-sprite ---------------------*/
   }
   ```

## Aggiunta di una voce nel modello di HTML {#adding-entry-in-the-html-template}

Infine, è necessario includere una voce nel pacchetto di sviluppo per ogni proprietà che si desidera aggiungere all&#39;attività. Per crearne uno, fai riferimento a Creazione del codice dell’area di lavoro di AEM Forms .

1. Copia `task.html`:

   * da: `/libs/ws/js/runtime/templates/`
   * a: `/apps/ws/js/runtime/templates/`

1. Aggiungi le nuove informazioni a `/apps/ws/js/runtime/templates/task.html`.

   Ad esempio, aggiungi sotto `div class="taskProperties"`:

   ```jsp
   <span class="stepname" alt="<%= $.t('task.stepname.value')%>" title = '<%= $.t("task.stepname.tooltip",{stepName:stepName})%>'/>
   ```
