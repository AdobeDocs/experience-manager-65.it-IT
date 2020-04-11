---
title: Hosting di due istanze dell'area di lavoro AEM Forms su un server
seo-title: Hosting di due istanze dell'area di lavoro AEM Forms su un server
description: In che modo gli amministratori LC possono personalizzare HTML WS per ospitare due istanze su un singolo server accessibile tramite URL diversi.
seo-description: In che modo gli amministratori LC possono personalizzare HTML WS per ospitare due istanze su un singolo server accessibile tramite URL diversi.
uuid: 0584f512-6b92-4418-b71c-93605cfa1927
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 1254a7c2-2c67-4661-803e-afd53e817916
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Hosting di due istanze dell&#39;area di lavoro AEM Forms su un server {#hosting-two-aem-forms-workspace-instances-on-one-server}

L’installazione e le impostazioni predefinite di AEM Forms consentono la disponibilità sul server di un’unica area di lavoro AEM Forms. Tuttavia, potrebbe essere necessario ospitare due istanze diverse dell&#39;area di lavoro AEM Forms su un singolo server AEM Forms. Le due istanze sono accessibili tramite URL diversi.

Gli amministratori di AEM Forms personalizzano l’area di lavoro per creare due URL diversi e rendere disponibili due aree di lavoro sullo stesso server. In questo articolo sulla personalizzazione, si presuppone che le due aree di lavoro siano accessibili in `https://'[server]:[port]'/lc/ws` e `https://'[server]:[port]':/lc/ws2`.

Per configurare l&#39;area di lavoro Moduli AEM, procedi come indicato di seguito.

1. Installa il pacchetto di sviluppo dell’area di lavoro AEM Forms sul server. Per istruzioni su come crearlo, consultate [dev package](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p).
1. Accedi a CRXDE Lite come amministratore, accedendo `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Copiare il nodo era in /content e incollare in /content. Rinominare il nodo in ws2. Fate clic su **[!UICONTROL Salva tutto]**. Nelle proprietà di questo nodo, modificare il valore di `sling:resourceType` su ws2. Fate clic su **[!UICONTROL Salva tutto]**.

1. Copiare la cartella era da /libs e incollare in /apps. Rinominate la cartella in ws2. Fate clic su **[!UICONTROL Salva tutto]**.
1. Nella `GET.jsp` pagina `/apps/ws2`, apportate le seguenti modifiche al codice. Sostituisci quanto segue

   ```
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" /><html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" />
   ```

   con il seguente codice

   ```
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. Nella `registry.js` parte `/apps/ws2/js`, modificate il percorso dei modelli in modo che faccia riferimento ai modelli in `/apps/ws2/js/runtime/templates`. Sostituire il seguente codice

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/libs/ws/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

   con il seguente codice

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/apps/ws2/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

1. In `userinfo.js` at `/apps/ws2/js/runtime/models` e `/apps/ws2/js/runtime/views`, modificare la stringa `/lc/content/ws` in `lc/content/ws2`.

1. In `/apps/ws2/js/runtime/services/service.js`, modificare il percorso della `getLocalizationData` funzione in modo che punti a `/lc/apps/ws2/Locale.html`.

1. Per fare riferimento a `pdf.html` una nuova area di lavoro, modificare il percorso di `pdf.html` in `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. Per fare riferimento `pdf.html` alla nuova area di lavoro, modificare i percorsi di `pdf.html` e `WsNextAdapter.swf` in `startprocess.html`, `taskdetails.html`e `processinstancehistory.html` in `/apps/ws2/js/runtime/templates`.

1. Copiate `/etc/map/ws` la cartella e incollatela in `/etc/map`. Rinominate la nuova cartella in ws2. Fate clic su Salva tutto.

1. Nelle proprietà di `ws2`, modificare il valore di `sling:redirect` in `content/ws2`.

1. Modificate il valore di `sling:match` in `^[^/\||]/[^/\||]/ws2$`.
