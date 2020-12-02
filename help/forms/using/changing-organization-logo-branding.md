---
title: Modifica del logo dell’organizzazione per il branding
seo-title: Modifica del logo dell’organizzazione per il branding
description: Per assegnare  marchio all’area di lavoro AEM Forms, personalizzate il logo dell’azienda.
seo-description: Per assegnare  marchio all’area di lavoro AEM Forms, personalizzate il logo dell’azienda.
uuid: f0c340ee-2e54-4bb0-9c30-383cc1bbadb8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2c651302-f4ef-4211-b897-f5942ed0ffb1
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# Modifica del logo dell&#39;organizzazione per il marchio {#changing-the-organization-logo-for-branding}

Il logo dell&#39;organizzazione viene visualizzato nell&#39;angolo superiore sinistro &#39;area di lavoro di AEM Forms. Per aggiornare il logo, seguire i passaggi [Generici di  personalizzazione dell&#39;area di lavoro AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) e quindi i passaggi seguenti.

1. Create un logo e denominate il file come `NewWorkspace.png`. Inserite il file di immagine nella cartella /apps/ws/images utilizzando un client WebDAV.

   >[!NOTE]
   >
   >La dimensione consigliata dell’immagine del logo è 218 px × 20 px.

   >[!NOTE]
   >
   >Per ulteriori informazioni sull&#39;accesso WebDAV, vedere [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

1. Fare riferimento alla nuova immagine del logo nel foglio di stile /apps/ws/css/newStyle.css aggiungendo il seguente stile.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
