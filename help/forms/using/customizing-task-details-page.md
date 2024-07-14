---
title: Personalizzazione della pagina dei dettagli dell’attività
description: Come personalizzare la pagina dei dettagli di un’attività nell’area di lavoro di AEM Forms per modificare le informazioni predefinite visualizzate su un’attività.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 48c24442-22d2-4d1a-9462-0aba78340281
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Personalizzazione della pagina dei dettagli dell’attività {#customizing-the-task-details-page}

La pagina dei dettagli di un&#39;attività contiene informazioni su un&#39;attività e sui relativi processi. È tuttavia possibile personalizzare la pagina dei dettagli dell&#39;operazione per aggiungere o eliminare informazioni.

È possibile aggiungere le seguenti informazioni alla pagina dei dettagli dell&#39;attività:

* Informazioni disponibili nell&#39;oggetto JSON di un&#39;attività (sezione Attività in [Descrizione oggetto JSON dell&#39;area di lavoro AEM Forms](/help/forms/using/html-workspace-json-object-description.md))
* Informazioni disponibili nell&#39;oggetto JSON di un&#39;istanza del processo (sezione Istanza del processo in [Descrizione oggetto JSON dell&#39;area di lavoro AEM Forms](/help/forms/using/html-workspace-json-object-description.md))

Per personalizzare la pagina dei dettagli dell&#39;operazione:

1. Segui [Passaggi generici per la personalizzazione dell&#39;area di lavoro AEM Forms.](/help/forms/using/generic-steps-html-workspace-customization.md)
1. Per visualizzare ulteriori informazioni, aggiungere coppie chiave-valore corrispondenti al file `translation.json` in `todo`blocco > `details`blocco > `app`blocco > [`required`blocco].

   Il [`required`blocco] fa riferimento ai blocchi disponibili, ad esempio il blocco di attività per le informazioni sulle attività, il blocco di processo per le informazioni sui processi e il blocco di attività corrente per le informazioni sulle attività in sospeso.

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

1. Copia `/libs/ws/js/runtime/templates/taskdetails.html` in `/apps/ws/js/runtime/templates/taskdetails.html`.

   Aggiungere le nuove informazioni a `/apps/ws/js/runtime/templates/taskdetails.html`. Ad esempio:

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
>Per personalizzare la pagina dei dettagli delle attività con le attività create nella scheda **Avvia processo** dell&#39;area di lavoro di AEM Forms, aggiungere le nuove informazioni a `/apps/ws/js/runtime/templates/startprocess.html`.
>
>Per aggiungere nuovi stili per le informazioni aggiunte nella pagina dei dettagli, modifica il file CSS utilizzando la sezione *Modifiche all&#39;interfaccia utente* in [Personalizzazione Workspace](changing-locale-user-interface.md).
