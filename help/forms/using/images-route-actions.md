---
title: Personalizzare le immagini utilizzate nelle azioni di indirizzamento
description: Come personalizzare le immagini utilizzate nelle azioni di indirizzamento nell’area di lavoro LiveCycle AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 687c6569-7189-4039-9c7a-bc29658a7756
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Personalizzare le immagini utilizzate nelle azioni di indirizzamento {#customize-images-used-in-route-actions}

Per personalizzare le immagini utilizzate nelle azioni di instradamento, eseguire i passaggi descritti in [Passaggi generici della personalizzazione](/help/forms/using/generic-steps-html-workspace-customization.md) seguito dai passaggi descritti in questo articolo.

## Immagini per le azioni del ciclo di lavorazione {#images-for-route-actions}

1. Aggiungi gli stili che definiscono le immagini nel CSS nella posizione seguente per le nuove azioni di indirizzamento:

   `/apps/ws/css/newStyle.css`

   Ad esempio: aggiungi un nuovo stile denominato `myStyle1`come mostrato di seguito e carica il file di immagine `myStyleIcon1.png` al `/apps/ws/image`s cartella utilizzando un client WebDAV.

   >[!NOTE]
   >
   >Per ulteriori informazioni, consulta [Accesso WebDAV](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=en).

   >[!NOTE]
   >
   >Preferisci che il nome dello stile sia uguale al nome dell’azione del percorso.

   ```css
   .myStyle1{
   
           background-image: url('../images/myStyleIcon1.png');
   
       }
   ```

## Popup azione attività Elenco attività {#task-list-task-action-popup}

1. Creare una finestra a comparsa per l&#39;azione dell&#39;elenco attività, vedere [Creazione del codice dell’area di lavoro di AEM Forms](introduction-customizing-html-workspace.md#building-html-workspace-code). Richiede di utilizzare il pacchetto di sviluppo.

1. Copia `/libs/ws/js/runtime/templates/task.html` a `/apps/ws/js/runtime/templates/task.html`.

1. Se il nome dello stile CSS è uguale al nome dell&#39;azione route proveniente dal server, modifica il seguente codice in `/apps/ws/js/runtime/templates/task.html`:

   ```jsp
   <%if(routeList == null){%>
               <li>
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li>
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   
   To
   
   <%if(routeList == null){%>
               <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li class="<%= availableCommands.directCommands[i]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   ```

1. Se il nome dello stile CSS è diverso dal nome dell&#39;azione di route proveniente dal server, modifica il seguente codice in `/apps/ws/js/runtime/templates/task.html`. Aggiunge una pila del `if-else` condizioni servlet per mappare lo stile con il nome dell&#39;azione route.

```jsp
<%if(routeList == null){%>
            <li>
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
            <li>
                <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
            </li>
            <%}%>
            <%}%>

To

<%if(routeList == null){%>
            <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
                <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                     <li class="myStyle1" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                     <li class="myStyle2" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}%>
            <%}%>
            <%}%>
```

## Popup azione attività Dettagli attività {#task-details-task-action-popup}

1. Copia `/libs/ws/js/runtime/templates/taskdetails.html` a `/apps/ws/js/runtime/templates/taskdetails.html`.

1. Se il nome dello stile CSS è uguale al nome dell&#39;azione route proveniente dal server, modifica il seguente codice in `/apps/ws/js/runtime/templates/taskdetails.html`:

   ```jsp
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                       <%}%>
   ```

1. Se il nome dello stile CSS è diverso dal nome dell&#39;azione di route proveniente dal server, modifica il seguente codice in `/apps/ws/js/runtime/templates/taskdetails.html`. Aggiunge una pila di `if-else` condizioni servlet per mappare lo stile con il nome dell&#39;azione route.

   ```jsp
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                   <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle1" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle2" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}%>
               <%}%>
   ```

1. Apri `/apps/ws/js/registry.js` per la modifica e cercare il testo seguente:
   `"text!/lc/libs/ws/js/runtime/templates/taskdetails.html"`

1. Sostituire il testo con quanto segue:
   `"text!/lc/apps/ws/js/runtime/templates/taskdetails.html"`
