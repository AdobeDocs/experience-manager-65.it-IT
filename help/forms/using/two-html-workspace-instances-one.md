---
title: Hosting di due istanze dell’area di lavoro AEM Forms su un server
seo-title: Hosting two AEM Forms workspace instances on one server
description: Come gli amministratori LC possono personalizzare HTML WS per ospitare due istanze su un singolo server accessibile tramite URL diversi.
seo-description: How LC administrators can customize HTML WS to host two instances on a single server accessible via different URLs.
uuid: 0584f512-6b92-4418-b71c-93605cfa1927
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 1254a7c2-2c67-4661-803e-afd53e817916
exl-id: 32a546fc-e33f-46f9-ac3b-45eca0e12239
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Hosting di due istanze dell’area di lavoro AEM Forms su un server {#hosting-two-aem-forms-workspace-instances-on-one-server}

L’installazione e le impostazioni predefinite di AEM Forms consentono la disponibilità sul server di una sola area di lavoro AEM Forms. Tuttavia, potrebbe essere necessario ospitare due istanze diverse dell’area di lavoro di AEM Forms su un singolo server AEM Forms. Le due istanze sono accessibili da URL diversi.

Gli amministratori di AEM Forms personalizzano l’area di lavoro per creare due URL diversi e rendere disponibili due aree di lavoro sullo stesso server. In questo articolo sulla personalizzazione, si presuppone che le due aree di lavoro siano accessibili in `https://'[server]:[port]'/lc/ws` e `https://'[server]:[port]':/lc/ws2`.

Segui questi passaggi per configurare l’area di lavoro AEM Forms.

1. Installa il pacchetto di sviluppo dell’area di lavoro AEM Forms sul server. Vedi [pacchetto di sviluppo](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p), per istruzioni su come crearlo.
1. Accedi a CRXDE Lite come amministratore, accedendo a `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Copia il nodo in /content e incolla in /content. Rinomina il nodo in ws2. Fai clic su **[!UICONTROL Salva tutto]**. Nelle proprietà di questo nodo, modifica il valore di `sling:resourceType` a ws2. Fai clic su **[!UICONTROL Salva tutto]**.

1. Copia la cartella da /libs e incolla in /apps. Rinomina la cartella in ws2. Fai clic su **[!UICONTROL Salva tutto]**.
1. In `GET.jsp` a `/apps/ws2`, apporta le seguenti modifiche al codice. Sostituisci quanto segue

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

1. In `registry.js` a `/apps/ws2/js`, cambia il percorso dei modelli per fare riferimento ai modelli in `/apps/ws2/js/runtime/templates`. Sostituisci il seguente codice

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

1. In `userinfo.js` a `/apps/ws2/js/runtime/models` e `/apps/ws2/js/runtime/views`, cambia stringa `/lc/content/ws` a `lc/content/ws2`.

1. In `/apps/ws2/js/runtime/services/service.js`, cambia il percorso in `getLocalizationData` funzione per puntare a `/lc/apps/ws2/Locale.html`.

1. Per fare riferimento a `pdf.html` del nuovo spazio di lavoro, cambia il percorso `pdf.html` in `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. Per fare riferimento a `pdf.html` del nuovo spazio di lavoro, cambiare i percorsi `pdf.html` e `WsNextAdapter.swf` in `startprocess.html`, `taskdetails.html`e `processinstancehistory.html` a `/apps/ws2/js/runtime/templates`.

1. Copia `/etc/map/ws` e incolla in `/etc/map`. Rinomina la nuova cartella in ws2. Fai clic su Salva tutto.

1. Nelle proprietà di `ws2`, cambia valore di `sling:redirect` a `content/ws2`.

1. Cambia valore di `sling:match` a `^[^/\||]/[^/\||]/ws2$`.
