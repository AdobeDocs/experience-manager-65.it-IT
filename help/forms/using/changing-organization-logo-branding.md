---
title: Modifica del logo dell’organizzazione per il branding
seo-title: Modifica del logo dell’organizzazione per il branding
description: Per assegnare un marchio all’area di lavoro AEM Forms, personalizzare il logo predefinito dell’organizzazione.
seo-description: Per assegnare un marchio all’area di lavoro AEM Forms, personalizzare il logo predefinito dell’organizzazione.
uuid: f0c340ee-2e54-4bb0-9c30-383cc1bbadb8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2c651302-f4ef-4211-b897-f5942ed0ffb1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Modifica del logo dell’organizzazione per il branding {#changing-the-organization-logo-for-branding}

Il logo dell&#39;organizzazione viene visualizzato nell&#39;angolo superiore sinistro dell&#39;area di lavoro AEM Forms. Per aggiornare il logo, segui i passaggi [Generici della personalizzazione](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) dell’area di lavoro AEM Forms e quindi i passaggi seguenti.

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

[Contattare il supporto](https://www.adobe.com/account/sign-in.supportportal.html)
