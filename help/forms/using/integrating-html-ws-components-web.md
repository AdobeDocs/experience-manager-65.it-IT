---
title: Integrazione dei componenti dell’area di lavoro di AEM Forms nelle applicazioni web
description: Come riutilizzare i componenti dell’area di lavoro di AEM Forms nelle tue applicazioni web per utilizzare le funzionalità e fornire un’integrazione perfetta.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: bb4a500d-c34f-4586-83f0-ad7ef69b4fb1
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# Integrazione dei componenti dell’area di lavoro di AEM Forms nelle applicazioni web {#integrating-aem-forms-workspace-components-in-web-applications}

Puoi utilizzare i [componenti](/help/forms/using/description-reusable-components.md) dell&#39;area di lavoro AEM Forms nella tua applicazione Web. L’implementazione di esempio seguente utilizza i componenti di un pacchetto di sviluppo per l’area di lavoro di AEM Forms installato in un’istanza CRX™ per creare un’applicazione web. Personalizza la soluzione qui sotto in base alle tue esigenze specifiche. L&#39;implementazione di esempio riutilizza `UserInfo`, `FilterList` e `TaskList` componenti all&#39;interno di un portale Web.

1. Accedere all&#39;ambiente CRXDE Lite in `https://'[server]:[port]'/lc/crx/de/`. Verifica che sia installato un pacchetto di sviluppo per l’area di lavoro di AEM Forms.
1. Creare un percorso `/apps/sampleApplication/wscomponents`.
1. Copia css, immagini, js/libs, js/runtime e js/registry.js

   * da `/libs/ws`
   * a `/apps/sampleApplication/wscomponents`.

1. Crea un file demo.js all’interno della cartella /apps/sampleApplication/wscomponents/js. Copia il codice da /libs/ws/js/main.js in demomain.js.
1. In demo.js, rimuovi il codice per inizializzare il router e aggiungi il seguente codice:

   ```javascript
   require(['initializer','runtime/util/usersession'],
       function(initializer, UserSession) {
           UserSession.initialize(
               function() {
                   // Render all the global components
                   initializer.initGlobal();
               });
       });
   ```

1. Creare un nodo in /content per nome `sampleApplication` e tipo `nt:unstructured`. Nelle proprietà di questo nodo aggiungere `sling:resourceType` di tipo String e valore `sampleApplication`. Nell&#39;elenco di controllo di accesso di questo nodo aggiungere una voce per `PERM_WORKSPACE_USER` che consenta i privilegi jcr:read. Inoltre, nell&#39;elenco di controllo di accesso di `/apps/sampleApplication` aggiungere una voce per `PERM_WORKSPACE_USER` che consenta i privilegi jcr:read.
1. In `/apps/sampleApplication/wscomponents/js/registry.js` aggiornare i percorsi da `/lc/libs/ws/` a `/lc/apps/sampleApplication/wscomponents/` per i valori del modello.
1. Nel file JSP della home page del portale in `/apps/sampleApplication/GET.jsp`, aggiungere il codice seguente per includere i componenti richiesti all&#39;interno del portale.

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   Includi anche i file CSS necessari per i componenti dell’area di lavoro di AEM Forms.

   >[!NOTE]
   >
   >Ogni componente viene aggiunto al tag componente (con class component) durante il rendering. Assicurati che la tua pagina principale contenga questi tag. Per ulteriori informazioni su questi tag di controllo di base, vedere il file `html.jsp` dell&#39;area di lavoro di AEM Forms.

1. Per personalizzare i componenti, potete estendere le viste esistenti per il componente richiesto nel modo seguente:

   ```javascript
   define([
       'jquery',
       'underscore',
       'backbone',
       'runtime/views/userinfo'],
       function($, _, Backbone, UserInfo){
           var demoUserInfo = UserInfo.extend({
               //override the functions to customize the functionality
               render: function() {
                   UserInfo.prototype.render.call(this); // call the render function of the super class
                   …
                   //other tasks
                   …
               }
           });
           return demoUserInfo;
   });
   ```

1. Modifica il CSS portale per configurare il layout, il posizionamento e lo stile dei componenti richiesti sul portale. Ad esempio, se vuoi mantenere il colore di sfondo nero per questo portale, puoi visualizzare bene il componente UserInfo. Per eseguire questa operazione, modificare il colore di sfondo in `/apps/sampleApplication/wscomponents/css/style.css` nel modo seguente:

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
