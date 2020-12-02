---
title: Integrazione  componenti dell’area di lavoro AEM Forms nelle applicazioni Web
seo-title: Integrazione  componenti dell’area di lavoro AEM Forms nelle applicazioni Web
description: Come riutilizzare  componenti dell'area di lavoro AEM Forms nelle proprie app Web per sfruttare le funzionalità e fornire un'integrazione stretta.
seo-description: Come riutilizzare  componenti dell'area di lavoro AEM Forms nelle proprie app Web per sfruttare le funzionalità e fornire un'integrazione stretta.
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Integrazione  componenti dell&#39;area di lavoro AEM Forms nelle applicazioni Web {#integrating-aem-forms-workspace-components-in-web-applications}

È possibile utilizzare  area di lavoro AEM Forms [componenti](/help/forms/using/description-reusable-components.md) nella propria applicazione Web. L&#39;implementazione di esempio seguente utilizza i componenti di un pacchetto di sviluppo  area di lavoro AEM Forms installato in un&#39;istanza CRX™ per creare un&#39;applicazione Web. Personalizza la soluzione indicata di seguito in base alle tue esigenze specifiche. L&#39;implementazione di esempio riutilizza `UserInfo`, `FilterList` e `TaskList`componenti all&#39;interno di un portale Web.

1. Accedete all&#39;ambiente CRXDE Lite in `https://'[server]:[port]'/lc/crx/de/`. Accertatevi di disporre di un pacchetto di sviluppo del percorso di lavoro AEM Forms  installato.
1. Create un percorso `/apps/sampleApplication/wscomponents`.
1. Copiate css, immagini, js/libs, js/runtime e js/registry.js

   * da `/libs/ws`
   * a `/apps/sampleApplication/wscomponents`.

1. Create un file dominio.js all&#39;interno della cartella /apps/sampleApplication/wscomponents/js. Copiate il codice da /libs/ws/js/main.js a download.js.
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

1. Create un nodo in /content in base al nome `sampleApplication` e digitate `nt:unstructured`. Nelle proprietà di questo nodo aggiungere `sling:resourceType` di tipo String e valore `sampleApplication`. Nell&#39;elenco Controllo di accesso di questo nodo aggiungere una voce per `PERM_WORKSPACE_USER` che consenta i privilegi jcr:read. Inoltre, nell&#39;elenco Controllo accesso di `/apps/sampleApplication` aggiungere una voce per `PERM_WORKSPACE_USER` che consenta i privilegi jcr:read.
1. In `/apps/sampleApplication/wscomponents/js/registry.js` aggiornare i percorsi da `/lc/libs/ws/` a `/lc/apps/sampleApplication/wscomponents/` per i valori dei modelli.
1. Nel file JSP della home page del portale in `/apps/sampleApplication/GET.jsp`, aggiungi il codice seguente per includere i componenti richiesti all&#39;interno del portale.

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   Includete anche i file CSS richiesti per i componenti dell&#39;area di lavoro di  AEM Forms.

   >[!NOTE]
   >
   >Ciascun componente viene aggiunto al tag del componente (con componente di classe) durante il rendering. Accertatevi che la pagina principale contenga questi tag. Per ulteriori informazioni su questi tag di controllo di base, vedere il file `html.jsp`  area di lavoro di AEM Forms.

1. Per personalizzare i componenti, potete estendere le viste esistenti per il componente richiesto come segue:

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

1. Modificate il CSS del portale per configurare il layout, il posizionamento e lo stile dei componenti richiesti sul portale. Ad esempio, per visualizzare correttamente il componente userInfo, si desidera mantenere il colore di sfondo nero per il portale. A tale scopo, è possibile modificare il colore di sfondo in `/apps/sampleApplication/wscomponents/css/style.css` nel modo seguente:

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
