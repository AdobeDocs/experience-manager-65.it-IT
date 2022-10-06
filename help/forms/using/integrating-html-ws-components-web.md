---
title: Integrazione dei componenti dell’area di lavoro AEM Forms nelle applicazioni web
seo-title: Integrating AEM Forms workspace components in web applications
description: Come riutilizzare i componenti dell’area di lavoro AEM Forms nelle tue applicazioni web per sfruttare le funzionalità e fornire un’integrazione stretta.
seo-description: How to reuse AEM Forms workspace components in your own webapps to leverage functionality and provide tight integration.
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
exl-id: bb4a500d-c34f-4586-83f0-ad7ef69b4fb1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# Integrazione dei componenti dell’area di lavoro AEM Forms nelle applicazioni web {#integrating-aem-forms-workspace-components-in-web-applications}

Puoi utilizzare l’area di lavoro AEM Forms [componenti](/help/forms/using/description-reusable-components.md) nella tua applicazione web. L&#39;implementazione di esempio seguente utilizza i componenti di un pacchetto di sviluppo dell&#39;area di lavoro AEM Forms installato su un&#39;istanza CRX™ per creare un&#39;applicazione web. Personalizza la soluzione riportata di seguito in base alle tue esigenze specifiche. L’implementazione di esempio viene riutilizzata `UserInfo`, `FilterList`e `TaskList`all’interno di un portale web.

1. Accedi all’ambiente CRXDE Lite all’indirizzo `https://'[server]:[port]'/lc/crx/de/`. Assicurati di avere installato un pacchetto di sviluppo del ritmo di lavoro di AEM Forms.
1. Creare un percorso `/apps/sampleApplication/wscomponents`.
1. Copia css, immagini, js/libs, js/runtime e js/registry.js

   * da `/libs/ws`
   * a `/apps/sampleApplication/wscomponents`.

1. Crea un file demomain.js all&#39;interno della cartella /apps/sampleApplication/wscomponents/js . Copia il codice da /libs/ws/js/main.js in demomain.js.
1. In demomain.js, rimuovi il codice per inizializzare Router e aggiungi il seguente codice:

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

1. Crea un nodo sotto /content per nome `sampleApplication` e tipo `nt:unstructured`. Nelle proprietà di questo nodo aggiungi `sling:resourceType` di tipo String e di valore `sampleApplication`. Nell&#39;elenco Controllo Accesso di questo nodo aggiungere una voce per `PERM_WORKSPACE_USER` abilitazione dei privilegi jcr:read. Inoltre, nell&#39;elenco di controllo accessi di `/apps/sampleApplication` aggiungi una voce per `PERM_WORKSPACE_USER` abilitazione dei privilegi jcr:read.
1. In `/apps/sampleApplication/wscomponents/js/registry.js` aggiorna percorsi da `/lc/libs/ws/` a `/lc/apps/sampleApplication/wscomponents/` per i valori del modello.
1. Nel file JSP della home page del portale in `/apps/sampleApplication/GET.jsp`, aggiungi il seguente codice per includere i componenti richiesti all’interno del portale.

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   Includere anche i file CSS richiesti per i componenti dell’area di lavoro di AEM Forms.

   >[!NOTE]
   >
   >Ogni componente viene aggiunto al tag componente (con componente classe) durante il rendering. Assicurati che la tua home page contenga questi tag. Consulta la sezione `html.jsp` file dell&#39;area di lavoro di AEM Forms per ulteriori informazioni su questi tag di controllo di base.

1. Per personalizzare i componenti, è possibile estendere le viste esistenti per il componente richiesto come segue:

   ```javascript
   define([
       ‘jquery’,
       ‘underscore’,
       ‘backbone’,
       ‘runtime/views/userinfo'],
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

1. Modifica il CSS del portale per configurare il layout, il posizionamento e lo stile dei componenti richiesti sul portale. Per visualizzare bene il componente userInfo, ad esempio, si desidera mantenere il colore di sfondo nero per il portale. Per farlo, modifica il colore di sfondo in `/apps/sampleApplication/wscomponents/css/style.css` come segue:

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
