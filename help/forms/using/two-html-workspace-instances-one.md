---
title: Hosting di due istanze  area di lavoro AEM Forms su un server
seo-title: Hosting di due istanze  area di lavoro AEM Forms su un server
description: In che modo gli amministratori LC possono personalizzare HTML WS per ospitare due istanze su un singolo server accessibile tramite URL diversi.
seo-description: In che modo gli amministratori LC possono personalizzare HTML WS per ospitare due istanze su un singolo server accessibile tramite URL diversi.
uuid: 0584f512-6b92-4418-b71c-93605cfa1927
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 1254a7c2-2c67-4661-803e-afd53e817916
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---


# Hosting di due istanze  area di lavoro AEM Forms su un server {#hosting-two-aem-forms-workspace-instances-on-one-server}

L&#39;installazione e le impostazioni predefinite di  AEM Forms consentono la disponibilità sul server di una sola area di lavoro  AEM Forms. Tuttavia, potrebbe essere necessario ospitare due istanze diverse dell&#39;area di lavoro  AEM Forms su un singolo server AEM Forms . Le due istanze sono accessibili tramite URL diversi.

 gli amministratori di AEM Forms personalizzano l’area di lavoro per creare due URL diversi e rendere disponibili due aree di lavoro sullo stesso server. In questo articolo di personalizzazione, si presuppone che le due aree di lavoro siano accessibili in `https://'[server]:[port]'/lc/ws` e `https://'[server]:[port]':/lc/ws2`.

Per configurare &#39;area di lavoro AEM Forms, effettuate le seguenti operazioni.

1. Installate il pacchetto dev di  area di lavoro AEM Forms sul server. Per istruzioni su come creare il pacchetto [dev](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p), vedere &lt;a0/>pacchetto dev&lt;a1/>.
1. Accedi al CRXDE Lite come amministratore, accedendo a `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Copiare il nodo era in /content e incollare in /content. Rinominare il nodo in ws2. Fare clic su **[!UICONTROL Salva tutto]**. Nelle proprietà di questo nodo, modificare il valore di `sling:resourceType` in ws2. Fare clic su **[!UICONTROL Salva tutto]**.

1. Copiare la cartella era da /libs e incollare in /apps. Rinominate la cartella in ws2. Fare clic su **[!UICONTROL Salva tutto]**.
1. In `GET.jsp` in `/apps/ws2`, apportare le seguenti modifiche al codice. Sostituisci quanto segue

   ```html
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

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. In `registry.js` all&#39;indirizzo `/apps/ws2/js`, modificare il percorso dei modelli per fare riferimento ai modelli all&#39;indirizzo `/apps/ws2/js/runtime/templates`. Sostituire il seguente codice

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

1. In `userinfo.js` alle `/apps/ws2/js/runtime/models` e `/apps/ws2/js/runtime/views`, modificare la stringa `/lc/content/ws` in `lc/content/ws2`.

1. In `/apps/ws2/js/runtime/services/service.js`, modificare il percorso della funzione `getLocalizationData` in modo che punti a `/lc/apps/ws2/Locale.html`.

1. Per fare riferimento a `pdf.html` della nuova area di lavoro, modificare il percorso di `pdf.html` in `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. Per fare riferimento a `pdf.html` della nuova area di lavoro, modificare i percorsi di `pdf.html` e `WsNextAdapter.swf` in `startprocess.html`, `taskdetails.html` e `processinstancehistory.html` in `/apps/ws2/js/runtime/templates`.

1. Copiate la cartella `/etc/map/ws` e incollatela in `/etc/map`. Rinominate la nuova cartella in ws2. Fate clic su Salva tutto.

1. Nelle proprietà di `ws2`, modificare il valore di `sling:redirect` in `content/ws2`.

1. Modificate il valore di `sling:match` in `^[^/\||]/[^/\||]/ws2$`.
