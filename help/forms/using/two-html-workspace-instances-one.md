---
title: Hosting di due istanze dell’area di lavoro AEM Forms su un server
description: Come gli amministratori LC possono personalizzare HTML WS per ospitare due istanze su un singolo server accessibile tramite URL diversi.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 32a546fc-e33f-46f9-ac3b-45eca0e12239
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---

# Hosting di due istanze dell’area di lavoro AEM Forms su un server {#hosting-two-aem-forms-workspace-instances-on-one-server}

L’installazione e le impostazioni predefinite di AEM Forms consentono di rendere disponibile una sola area di lavoro AEM Forms sul server. Tuttavia, potrebbe essere necessario ospitare due diverse istanze dell’area di lavoro di AEM Forms su un singolo server AEM Forms. Le due istanze sono accessibili da URL diversi.

Gli amministratori di AEM Forms personalizzano l’area di lavoro per creare due URL diversi e rendere disponibili due aree di lavoro sullo stesso server. In questo articolo di personalizzazione, si può presumere che le due aree di lavoro siano accessibili all’indirizzo `https://'[server]:[port]'/lc/ws` e `https://'[server]:[port]':/lc/ws2`.

Per configurare l’area di lavoro di AEM Forms, segui la procedura riportata di seguito.

1. Installa il pacchetto di sviluppo dell’area di lavoro AEM Forms sul server. Consulta [pacchetto di sviluppo](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p), per istruzioni su come crearlo.
1. Accedi a CRXDE Liti come amministratore, accedendo a `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Copia il nodo ws in /content e incolla in /content. Rinomina il nodo in ws2. Clic **[!UICONTROL Salva tutto]**. Nelle proprietà di questo nodo, modifica il valore di `sling:resourceType` a ws2. Clic **[!UICONTROL Salva tutto]**.

1. Copia la cartella ws da /libs e incolla in /apps. Rinominare la cartella ws2. Clic **[!UICONTROL Salva tutto]**.
1. In entrata `GET.jsp` a `/apps/ws2`, apporta le seguenti modifiche al codice. Sostituisci quanto segue

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

1. In entrata `registry.js` a `/apps/ws2/js`, modifica il percorso dei modelli per fare riferimento ai modelli in `/apps/ws2/js/runtime/templates`. Sostituisci il seguente codice

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

1. In entrata `userinfo.js` a `/apps/ws2/js/runtime/models` e `/apps/ws2/js/runtime/views`, modifica stringa `/lc/content/ws` a `lc/content/ws2`.

1. In entrata `/apps/ws2/js/runtime/services/service.js`, modifica il percorso in `getLocalizationData` funzione per puntare a `/lc/apps/ws2/Locale.html`.

1. Per fare riferimento `pdf.html` del nuovo Workspace, modifica il percorso di `pdf.html` in `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. Per fare riferimento `pdf.html` del nuovo Workspace, modifica i percorsi di `pdf.html` e `WsNextAdapter.swf` in `startprocess.html`, `taskdetails.html`, e `processinstancehistory.html` a `/apps/ws2/js/runtime/templates`.

1. Copia `/etc/map/ws` cartella e incolla in `/etc/map`. Rinomina la nuova cartella in ws2. Fai clic su Salva tutto.

1. Nelle proprietà di `ws2`, modifica il valore di `sling:redirect` a `content/ws2`.

1. Modifica il valore di `sling:match` a `^[^/\||]/[^/\||]/ws2$`.
