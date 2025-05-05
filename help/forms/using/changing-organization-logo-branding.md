---
title: Modifica del logo organizzazione per il branding
description: Per aggiungere un marchio all’area di lavoro di AEM Forms, fornisci il logo della tua organizzazione personalizzando il logo predefinito.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Modifica del logo organizzazione per il branding {#changing-the-organization-logo-for-branding}

Il logo dell’organizzazione viene visualizzato nell’angolo superiore sinistro dell’area di lavoro AEM Forms. Per aggiornare il logo, segui i [passaggi generici della personalizzazione dell&#39;area di lavoro di AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) e quindi i passaggi seguenti.

1. Creare un logo e assegnare al file il nome `NewWorkspace.png`. Inserire il file immagine nella cartella /apps/ws/images utilizzando un client WebDAV.

   >[!NOTE]
   >
   >Le dimensioni consigliate per l&#39;immagine del logo sono 218 × 20 px.

   >[!NOTE]
   >
   >Per ulteriori informazioni, vedere [Accesso WebDAV](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=it).

   [Accesso WebDAV](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=it)

1. Fare riferimento alla nuova immagine del logo nel foglio di stile all&#39;indirizzo /apps/ws/css/newStyle.css aggiungendo il seguente stile.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
