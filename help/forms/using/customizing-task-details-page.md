---
title: Personalizzazione della pagina dei dettagli dell’attività
description: Come personalizzare la pagina dei dettagli di un’attività nell’area di lavoro di AEM Forms per modificare le informazioni predefinite visualizzate su un’attività.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 48c24442-22d2-4d1a-9462-0aba78340281
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Personalizzazione della pagina dei dettagli dell’attività {#customizing-the-task-details-page}

La pagina dei dettagli di un&#39;attività contiene informazioni su un&#39;attività e sui relativi processi. È tuttavia possibile personalizzare la pagina dei dettagli dell&#39;operazione per aggiungere o eliminare informazioni.

È possibile aggiungere le seguenti informazioni alla pagina dei dettagli dell&#39;attività:

* Informazioni disponibili nell’oggetto JSON di un’attività (sezione Attività in [Descrizione oggetto JSON dell’area di lavoro di AEM Forms](/help/forms/using/html-workspace-json-object-description.md))
* Informazioni disponibili nell’oggetto JSON di un’istanza di processo (sezione Istanza di processo in [Descrizione oggetto JSON dell’area di lavoro di AEM Forms](/help/forms/using/html-workspace-json-object-description.md))

Per personalizzare la pagina dei dettagli dell&#39;operazione:

1. Segui [Passaggi generici per la personalizzazione dell’area di lavoro AEM Forms.](/help/forms/using/generic-steps-html-workspace-customization.md)
1. Per visualizzare ulteriori informazioni, aggiungi le coppie chiave-valore corrispondenti alla `translation.json` file in `todo`blocco > `details`blocco > `app`blocco > [`required`blocco].

   Il [`required`blocco] fa riferimento ai blocchi disponibili, ad esempio il blocco task per le informazioni sul task, il blocco processo per le informazioni sul processo e il blocco task corrente per le informazioni sui task in sospeso.

   Ad esempio, per aggiungere informazioni sulla selezione route obbligatoria nella pagina dei dettagli dell&#39;attività, è possibile aggiungere la seguente coppia chiave-valore nel blocco dell&#39;attività:

   ```json
   "todo" : {
       .
       .
       .
       "details" : {
           .
           .
           "task" : {
               .
               .
               "RouteSelectionRequired" : "Route Selection Required"
           }
       }
   }
   ```

   >[!NOTE]
   >
   >Aggiungi coppie chiave-valore corrispondenti per tutte le lingue supportate.

1. Copia `/libs/ws/js/runtime/templates/taskdetails.html` a `/apps/ws/js/runtime/templates/taskdetails.html`.

   Aggiungi le nuove informazioni a `/apps/ws/js/runtime/templates/taskdetails.html`. Ad esempio:

   ```css
   <div class="detailsContainer">
       .
       .
       <ul>
           .
           .
           <li>
               <label for="routeSelectionRequired" title="<%= $.t('todo.details.task.RouteSelectionRequired')%>"><%= $.t('todo.details.task.RouteSelectionRequired')%></label>
               <div>
                   <span id="routeSelectionRequired"><%= isRouteSelectionRequired != null ? isRouteSelectionRequired : ''%></span>
               </div>
           </li>
           .
           .
       </ul>
   </div>
   ```

1. Apri /apps/ws/js/registry.js per la modifica.

   Cerca e sostituisci `text!/lc/libs/ws/js/runtime/templates/taskdetails.html` con `text!/lc/apps/ws/js/runtime/templates/taskdetails.html`.

>[!NOTE]
>
>Per personalizzare la pagina dei dettagli delle operazioni con le operazioni create in **Avvia processo** dell’area di lavoro di AEM Forms, aggiungi le nuove informazioni a `/apps/ws/js/runtime/templates/startprocess.html`.
>
>Per aggiungere nuovi stili per le informazioni aggiunte nella pagina dei dettagli, modifica il file CSS utilizzando *Modifiche all’interfaccia utente* sezione in [Personalizzazione di Workspace](changing-locale-user-interface.md).
