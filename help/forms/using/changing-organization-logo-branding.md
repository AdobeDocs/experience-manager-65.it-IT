---
title: Modifica del logo dell’organizzazione per il branding
description: Per aggiungere un marchio all’area di lavoro di AEM Forms, fornisci il logo della tua organizzazione personalizzando il logo predefinito.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
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
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 9%
---
# Modifica del logo dell’organizzazione per il branding {#changing-the-organization-logo-for-branding}

Il logo dell’organizzazione viene visualizzato nell’angolo superiore sinistro dell’area di lavoro AEM Forms. Per aggiornare il logo, segui i [passaggi generici della personalizzazione dell&#39;area di lavoro di AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) e quindi i passaggi seguenti.

1. Creare un logo e assegnare al file il nome `NewWorkspace.png`. Inserire il file immagine nella cartella /apps/ws/images utilizzando un client WebDAV.

   >[!NOTE]
   >
   >Le dimensioni consigliate per l&#39;immagine del logo sono 218 × 20 px.

   >[!NOTE]
   >
   >Per ulteriori informazioni, vedere [Accesso WebDAV](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=it).

   [Accesso WebDav](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=it)

1. Fare riferimento alla nuova immagine del logo nel foglio di stile all&#39;indirizzo /apps/ws/css/newStyle.css aggiungendo il seguente stile.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
