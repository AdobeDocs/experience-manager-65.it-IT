---
title: Hosting di due istanze dell’area di lavoro di AEM Forms su un server
description: Come gli amministratori LC possono personalizzare HTML WS per ospitare due istanze su un singolo server accessibile tramite URL diversi.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 32a546fc-e33f-46f9-ac3b-45eca0e12239
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 5%
---
# Hosting di due istanze dell’area di lavoro di AEM Forms su un server {#hosting-two-aem-forms-workspace-instances-on-one-server}

L’installazione e le impostazioni predefinite di AEM Forms consentono di rendere disponibile una sola area di lavoro AEM Forms sul server. Tuttavia, potrebbe essere necessario ospitare due diverse istanze dell’area di lavoro di AEM Forms su un singolo server AEM Forms. Le due istanze sono accessibili da URL diversi.

Gli amministratori di AEM Forms personalizzano l’area di lavoro per creare due URL diversi e rendere disponibili due aree di lavoro sullo stesso server. In questo articolo di personalizzazione si può presumere che le due aree di lavoro siano accessibili alle `https://'[server]:[port]'/lc/ws` e `https://'[server]:[port]':/lc/ws2`.

Per configurare l’area di lavoro di AEM Forms, segui la procedura riportata di seguito.

1. Installa il pacchetto di sviluppo dell’area di lavoro AEM Forms sul server. Per istruzioni sulla creazione, vedere [pacchetto di sviluppo](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p).
1. Accedere a CRXDE Lite come amministratore accedendo a `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Copia il nodo ws in /content e incolla in /content. Rinomina il nodo in ws2. Fai clic su **[!UICONTROL Salva tutto]**. Nelle proprietà di questo nodo, modificare il valore di `sling:resourceType` in ws2. Fai clic su **[!UICONTROL Salva tutto]**.

1. Copia la cartella ws da /libs e incolla in /apps. Rinominare la cartella ws2. Fai clic su **[!UICONTROL Salva tutto]**.
1. In `GET.jsp` alle `/apps/ws2`, apporta le seguenti modifiche al codice. Sostituisci quanto segue

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

1. In `registry.js` alle `/apps/ws2/js`, cambia il percorso dei modelli in modo che faccia riferimento ai modelli in `/apps/ws2/js/runtime/templates`. Sostituisci il seguente codice

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

1. In `/apps/ws2/js/runtime/services/service.js`, modificare il percorso nella funzione `getLocalizationData` in modo che punti a `/lc/apps/ws2/Locale.html`.

1. Per fare riferimento a `pdf.html` del nuovo Workspace, modificare il percorso di `pdf.html` in `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. Per fare riferimento a `pdf.html` del nuovo Workspace, modificare i percorsi di `pdf.html` e `WsNextAdapter.swf` in `startprocess.html`, `taskdetails.html` e `processinstancehistory.html` alle `/apps/ws2/js/runtime/templates`.

1. Copiare la cartella `/etc/map/ws` e incollarla in `/etc/map`. Rinomina la nuova cartella in ws2. Fai clic su Salva tutto.

1. Nelle proprietà di `ws2`, modificare il valore di `sling:redirect` in `content/ws2`.

1. Cambia il valore di `sling:match` in `^[^/\||]/[^/\||]/ws2$`.
