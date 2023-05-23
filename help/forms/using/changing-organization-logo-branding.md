---
title: Modifica del logo organizzazione per il branding
seo-title: Changing the organization logo for branding
description: Per aggiungere un marchio all’area di lavoro di AEM Forms, fornisci il logo della tua organizzazione personalizzando il logo predefinito.
seo-description: To brand AEM Forms workspace provide the logo of your organization by customizing the default logo.
uuid: f0c340ee-2e54-4bb0-9c30-383cc1bbadb8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2c651302-f4ef-4211-b897-f5942ed0ffb1
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 6%

---

# Modifica del logo organizzazione per il branding {#changing-the-organization-logo-for-branding}

Il logo dell’organizzazione viene visualizzato nell’angolo superiore sinistro dell’area di lavoro AEM Forms. Per aggiornare il logo, attenersi alla [Passaggi generici della personalizzazione di AEM Forms Workspace](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) e quindi i seguenti passaggi.

1. Creare un logo e denominare il file come `NewWorkspace.png`. Inserire il file immagine nella cartella /apps/ws/images utilizzando un client WebDAV.

   >[!NOTE]
   >
   >Le dimensioni consigliate per l&#39;immagine del logo sono 218 × 20 px.

   >[!NOTE]
   >
   >Per ulteriori informazioni sull&#39;accesso WebDAV, vedere [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=it).

1. Fare riferimento alla nuova immagine del logo nel foglio di stile all&#39;indirizzo /apps/ws/css/newStyle.css aggiungendo il seguente stile.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
