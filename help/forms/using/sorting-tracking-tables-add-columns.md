---
title: Personalizzare le tabelle di tracciamento
seo-title: Personalizzare le tabelle di tracciamento
description: Procedura per personalizzare la visualizzazione dei dettagli dei processi utente nella tabella delle attività visualizzata nella scheda di tracciamento dell’area di lavoro di  AEM Forms.
seo-description: Procedura per personalizzare la visualizzazione dei dettagli dei processi utente nella tabella delle attività visualizzata nella scheda di tracciamento dell’area di lavoro di  AEM Forms.
uuid: 13d6ebf2-99d5-434f-85f9-b0cba5f5751a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: bb7a6e9f-4f28-4d97-8a0c-949259fd6857
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 3%

---


# Personalizzare le tabelle di tracciamento{#customize-tracking-tables}

La scheda di tracciamento nellarea di lavoro AEM Forms viene utilizzata per visualizzare i dettagli delle istanze del processo in cui è coinvolto l&#39;utente che ha effettuato l&#39;accesso. Per visualizzare le tabelle di tracciamento, selezionare innanzitutto un nome di processo nel riquadro a sinistra per visualizzare l&#39;elenco delle istanze nel riquadro centrale. Selezionare un&#39;istanza di processo per visualizzare nel riquadro a destra una tabella delle attività generate dall&#39;istanza. Per impostazione predefinita, nelle colonne della tabella sono visualizzati i seguenti attributi attività (l&#39;attributo corrispondente nel modello attività è indicato tra parentesi):

* ID ( `taskId`)
* Nome ( `stepName`)
* Istruzioni ( `instructions`)
* Azione selezionata ( `selectedRoute`)
* Ora di creazione ( `createTime`)
* Tempo di completamento ( `completeTime`)
* Proprietario ( `currentAssignment.queueOwner`)

Gli attributi rimanenti nel modello attività disponibili per la visualizzazione nella tabella delle attività sono:

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
   <td><p>savedFormCount</p> </td>
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
   <td><p>creatingId</p> </td>
   <td><p>isVisible</p> </td>
   <td><p>serviceTitle</p> </td>
  </tr>
  <tr>
   <td><p>currentAssignment</p> </td>
   <td><p>nextPromemoria</p> </td>
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
   <td><p>supportedSave</p> </td>
  </tr>
  <tr>
   <td><p>isApprovalUI</p> </td>
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

Per le seguenti personalizzazioni nella tabella delle attività, è necessario apportare modifiche semantiche nel codice sorgente. Consultate [Introduzione alla personalizzazione &#39;area di lavoro AEM Forms](/help/forms/using/introduction-customizing-html-workspace.md) per informazioni su come apportare modifiche semantiche utilizzando l&#39;SDK dell&#39;area di lavoro e creare un pacchetto ridotto dall&#39;origine modificata.

## Modifica delle colonne di tabella e relativo ordine {#changing-table-columns-and-their-order}

1. Per modificare gli attributi attività visualizzati nella tabella e il relativo ordine, configurate il file /ws/js/runtime/templates/processinstancehistory.html :

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

Per ordinare la tabella dell&#39;elenco delle attività quando si fa clic sull&#39;intestazione della colonna:

1. Registrare un gestore di clic per `.fixedTaskTableHeader th` nel file `js/runtime/views/processinstancehistory.js`.

   ```javascript
   events: {
       //other handlers
       "click .fixedTaskTableHeader th": "onTaskTableHeaderClick",
       //other handlers
   }
   ```

   Nel gestore, richiamare la funzione `onTaskTableHeaderClick` di `js/runtime/util/history.js`.

   ```javascript
   onTaskTableHeaderClick: function (event) {
           history.onTaskTableHeaderClick(event);
   }
   ```

1. Esporre il metodo `TaskTableHeaderClick` in `js/runtime/util/history.js`.

   Il metodo trova l&#39;attributo task dall&#39;evento click, ordina l&#39;elenco task su tale attributo ed esegue il rendering della tabella task con l&#39;elenco task ordinato.

   L&#39;ordinamento viene eseguito utilizzando la funzione di ordinamento Backbone nella raccolta di elenchi di task fornendo una funzione di confronto.

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
