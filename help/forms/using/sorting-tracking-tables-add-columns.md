---
title: Personalizzare le tabelle di tracciamento
seo-title: Customize tracking tables
description: Come personalizzare la visualizzazione dei dettagli dei processi utente nella tabella delle attività visualizzata nella scheda di tracciamento di AEM Forms workspace.
seo-description: How-to customize the display of the details of user processes in the task table displayed in the tracking tab of AEM Forms workspace.
uuid: 13d6ebf2-99d5-434f-85f9-b0cba5f5751a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: bb7a6e9f-4f28-4d97-8a0c-949259fd6857
exl-id: 9ab657cc-fa8e-4168-8a68-e38ac5c51b29
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 3%

---

# Personalizzare le tabelle di tracciamento{#customize-tracking-tables}

La scheda di tracciamento nell’area di lavoro di AEM Forms viene utilizzata per visualizzare i dettagli delle istanze del processo in cui è coinvolto l’utente connesso. Per visualizzare le tabelle di tracciamento, seleziona innanzitutto un nome di processo nel riquadro a sinistra per visualizzare l’elenco delle istanze nel riquadro centrale. Selezionare un&#39;istanza di processo per visualizzare una tabella delle attività generate da questa istanza nel riquadro a destra. Per impostazione predefinita, le colonne della tabella visualizzano i seguenti attributi di attività (l&#39;attributo corrispondente nel modello di task è indicato tra parentesi):

* ID ( `taskId`)
* Nome ( `stepName`)
* Istruzioni ( `instructions`)
* Azione selezionata ( `selectedRoute`)
* Tempo di creazione ( `createTime`)
* Ora di completamento ( `completeTime`)
* Proprietario ( `currentAssignment.queueOwner`)

Gli attributi rimanenti nel modello di task disponibili per la visualizzazione nella tabella di task sono:

<table>
 <tbody>
  <tr>
   <td><p>actionInstanceId</p> </td>
   <td><p>isOpenFullScreen</p> </td>
   <td><p>promemoriaCount</p> </td>
  </tr>
  <tr>
   <td><p>classOfTask</p> </td>
   <td><p>isOwner</p> </td>
   <td><p>routeList</p> </td>
  </tr>
  <tr>
   <td><p>consultareGroupId</p> </td>
   <td><p>isRouteSelectionRequired</p> </td>
   <td><p>saveFormCount</p> </td>
  </tr>
  <tr>
   <td><p>contentType</p> </td>
   <td><p>isShowAttachments</p> </td>
   <td><p>serializedImageTicket</p> </td>
  </tr>
  <tr>
   <td><p>createTime</p> </td>
   <td><p>isStartTask</p> </td>
   <td><p>serviceName</p> </td>
  </tr>
  <tr>
   <td><p>createdId</p> </td>
   <td><p>isVisible</p> </td>
   <td><p>serviceTitle</p> </td>
  </tr>
  <tr>
   <td><p>currentAssignment</p> </td>
   <td><p>nextReminder</p> </td>
   <td><p>showACLActions</p> </td>
  </tr>
  <tr>
   <td><p>scadenza</p> </td>
   <td><p>numForms</p> </td>
   <td><p>showDirectActions</p> </td>
  </tr>
  <tr>
   <td><p>descrizione</p> </td>
   <td><p>numFormsToBeSaved</p> </td>
   <td><p>stato</p> </td>
  </tr>
  <tr>
   <td><p>displayName</p> </td>
   <td><p>outOfOfficeUserId</p> </td>
   <td><p>summaryUrl</p> </td>
  </tr>
  <tr>
   <td><p>forwardGroupId</p> </td>
   <td><p>outOfOfficeUserName</p> </td>
   <td><p>supportSave</p> </td>
  </tr>
  <tr>
   <td><p>isApprovazioneUI</p> </td>
   <td><p>priority</p> </td>
   <td><p>taskACL</p> </td>
  </tr>
  <tr>
   <td><p>isCustomUI</p> </td>
   <td><p>processInstanceId</p> </td>
   <td><p>taskFormType</p> </td>
  </tr>
  <tr>
   <td><p>isDefaultImage</p> </td>
   <td><p>processInstanceStatus</p> </td>
   <td><p>taskUserInfo</p> </td>
  </tr>
  <tr>
   <td><p>isLocked</p> </td>
   <td><p>processVariables</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p>isMustOpenToComplete</p> </td>
   <td><p>readerSubmitOptions</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

Per le seguenti personalizzazioni nella tabella delle attività, è necessario apportare modifiche semantiche nel codice sorgente. Vedi [Introduzione alla personalizzazione dell’area di lavoro di AEM Forms](/help/forms/using/introduction-customizing-html-workspace.md) per sapere come apportare modifiche semantiche utilizzando l’SDK di workspace e creare un pacchetto minimizzato dall’origine modificata.

## Modifica dell’ordine delle colonne delle tabelle {#changing-table-columns-and-their-order}

1. Per modificare gli attributi delle attività visualizzati nella tabella e il relativo ordine, configura il file /ws/js/runtime/templates/processinstancehistory.html :

   ```html
   <table>
       <thead>
           <tr>
               <!-- put the column headings in order here, for example-->
               <th><%= $.t('history.fixedTaskTableHeader.taskName')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskInstructions')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskRoute')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskCreateTime')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskCompleteTime')%></th>
           </tr>
       </thead>
   </table>
   ```

   ```html
   <table>
       <tbody>
           <%_.each(obj, function(task){%>
           <tr>
               <!-- Put the task attributes in the order of headings, for example -->
               <td><%= task.stepName %></td>
               <td><%= task.instructions %></td>
               <td><%= !task.selectedRoute?'':(task.selectedRoute=='null'?'Default':task.selectedRoute) %></td>
               <td><%= task.createTime?task.formattedCreateTime:'' %></td>
               <td><%= task.completeTime? task.formattedCompleteTime:'' %></td>
           </tr>
           <%});%>
       </tbody>
   </table>
   ```

## Ordinamento di una tabella di tracciamento {#sorting-a-tracking-table}

Per ordinare la tabella dell’elenco delle attività facendo clic sull’intestazione della colonna:

1. Registra un gestore di clic per `.fixedTaskTableHeader th` nel file `js/runtime/views/processinstancehistory.js`.

   ```javascript
   events: {
       //other handlers
       "click .fixedTaskTableHeader th": "onTaskTableHeaderClick",
       //other handlers
   }
   ```

   Nel gestore, richiama il `onTaskTableHeaderClick` funzione `js/runtime/util/history.js`.

   ```javascript
   onTaskTableHeaderClick: function (event) {
           history.onTaskTableHeaderClick(event);
   }
   ```

1. Esporre le `TaskTableHeaderClick` metodo in `js/runtime/util/history.js`.

   Il metodo trova l&#39;attributo task dall&#39;evento click, ordina l&#39;elenco task su tale attributo ed esegue il rendering della tabella task con l&#39;elenco task ordinato.

   L&#39;ordinamento viene eseguito utilizzando la funzione di ordinamento Backbone nell&#39;insieme tasklist fornendo una funzione di confronto.

   ```javascript
       return {
           //other methods
           onTaskTableHeaderClick  : onTaskTableHeaderClick,
           //other methods
       };
   ```

   ```javascript
   onTaskTableHeaderClick = function (event) {
           var target = $(event.target),
            comparator,
               attribute;
           if(target.hasClass('taskName')){
            attribute = 'stepName';
           } else if(target.hasClass('taskInstructions')){
               attribute = 'instructions';
           } else if(target.hasClass('taskRoute')){
               attribute = 'selectedRoute';
           } else if(target.hasClass('taskCreateTime')){
               attribute = 'createTime';
           } else if(target.hasClass('taskCompleteTime')){
               attribute = 'completeTime';
           }
           taskList.comparator = function (task) {
            return task.get(attribute);
           };
           taskList.sort();
           render();
       };
   ```
