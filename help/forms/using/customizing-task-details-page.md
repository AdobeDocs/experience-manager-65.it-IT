---
title: Personalizzazione della pagina dei dettagli dell’attività
seo-title: Personalizzazione della pagina dei dettagli dell’attività
description: Come personalizzare la pagina dei dettagli dell’attività nell’area di lavoro  AEM Forms per modificare le informazioni predefinite visualizzate su un’attività.
seo-description: Come personalizzare la pagina dei dettagli dell’attività nell’area di lavoro  AEM Forms per modificare le informazioni predefinite visualizzate su un’attività.
uuid: d85fae55-8e66-4595-8560-5485622b6841
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 16e57cf6-aaa1-406d-a6ad-71ec60b15386
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Personalizzazione della pagina dei dettagli dell&#39;attività {#customizing-the-task-details-page}

La pagina dei dettagli dell&#39;attività contiene informazioni su un&#39;attività e sui relativi processi. Tuttavia, potete personalizzare la pagina dei dettagli dell’attività per aggiungere o eliminare informazioni.

È possibile aggiungere le seguenti informazioni alla pagina dei dettagli dell&#39;attività:

* Informazioni disponibili nell&#39;oggetto JSON di un&#39;attività (sezione Attività in [ area di lavoro AEM Forms JSON Object Description](/help/forms/using/html-workspace-json-object-description.md))
* Informazioni disponibili nell&#39;oggetto JSON di un&#39;istanza di processo (sezione dell&#39;istanza di processo in [ area di lavoro AEM Forms JSON Object Description](/help/forms/using/html-workspace-json-object-description.md))

Per personalizzare la pagina dei dettagli dell’attività:

1. Seguite i passaggi [Generici per  personalizzazione dell&#39;area di lavoro AEM Forms.](/help/forms/using/generic-steps-html-workspace-customization.md)
1. Per visualizzare ulteriori informazioni, aggiungere le coppie chiave-valore corrispondenti al file `translation.json` in `todo`block > `details`block > `app`block > [ `required`block].

   Il [ `required`block] fa riferimento ai blocchi disponibili, ad esempio il blocco attività per le informazioni sulle attività, il blocco di processo per le informazioni sul processo e il blocco attività in corso per le informazioni sulle attività in sospeso.

   Ad esempio, per aggiungere informazioni sulla selezione dell&#39;route richiesta nella pagina dei dettagli dell&#39;attività, è possibile aggiungere la coppia chiave-valore seguente nel blocco attività:

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
   >Aggiungete le coppie chiave-valore corrispondenti per tutte le lingue supportate.

1. Copiare `/libs/ws/js/runtime/templates/taskdetails.html` in `/apps/ws/js/runtime/templates/taskdetails.html`.

   Aggiungete le nuove informazioni a `/apps/ws/js/runtime/templates/taskdetails.html`. Esempio:

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

1. Aprite /apps/ws/js/registry.js per la modifica.

   Cercare e sostituire `text!/lc/libs/ws/js/runtime/templates/taskdetails.html` con `text!/lc/apps/ws/js/runtime/templates/taskdetails.html`.

>[!NOTE]
>
>Per personalizzare la pagina dei dettagli dell&#39;attività con le attività create nella scheda **Avvia processo** &#39;area di lavoro AEM Forms, aggiungere le nuove informazioni a `/apps/ws/js/runtime/templates/startprocess.html`.
>
>Per aggiungere nuovi stili per le informazioni aggiunte nella pagina dei dettagli, modificate il file CSS utilizzando la sezione *Modifiche all&#39;interfaccia utente* in [Personalizzazione area di lavoro](changing-locale-user-interface.md).
