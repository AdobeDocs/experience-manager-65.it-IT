---
title: Modifica del contenuto della pagina zero in Designer
description: Sapete come modificare il messaggio visualizzato sulla pagina zero di un PDF XFA quando lo si visualizza in un visualizzatore non Adobe PDF?
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Forms Designer,Designer
exl-id: 466b7e85-a2f8-4e1e-8afc-1566b0ccb84c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 1af3c3d4-88d7-5e0f-813c-eb70824bfcdd
    internal-label: Forms Designer
  - id: 794033c1-20ea-55a4-a8a6-b1107e12deb0
    internal-label: Designer
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
source-wordcount: '232'
ht-degree: 6%
---
# Modifica del contenuto della pagina zero in Designer {#changing-page-zero-content-in-designer}

Il contenuto Pagina zero viene visualizzato per impostazione predefinita quando un visualizzatore non Adobe PDF, ad esempio il visualizzatore PDF predefinito in [!DNL Chrome] o [!DNL Firefox], non è in grado di leggere il contenuto del modulo PDF/XFA. Di seguito viene visualizzato il messaggio predefinito Pagina zero.

![defaultpage0message](assets/defaultpage0message.png)

La versione [!DNL AEM Forms] di Designer consente di modificare il messaggio visualizzato a pagina zero. Per modificare il messaggio Pagina zero, effettuare le seguenti operazioni:

1. Verificare che sia installata la versione [!DNL AEM Forms] di Designer. Puoi controllare la versione dalla schermata Informazioni su di Designer.

1. Aprire il modulo di cui si desidera modificare il contenuto Pagina zero.

1. Fare clic su **[!UICONTROL File]** > **[!UICONTROL Proprietà modulo]**.

1. Nella finestra di dialogo [!UICONTROL Proprietà modulo], fai clic su ![più](assets/plus.png) (icona Più) per aggiungere una proprietà personalizzata.

1. Specificare **_pagezerocontent** come nome della proprietà.
1. Aggiungi come valore il nuovo messaggio Pagina zero, in formato Testo formattato. Ad esempio:


   `<body xmlns="http://www.w3.org/1999/xhtml" xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </span></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </span>https://www.adobe.com/go/reader_download_it.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </span></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </span>https://www.adobe.com/go/acrreader_it.</p></body>`

1. Salvare il modulo come PDF.

1. Visualizza il PDF Form nel browser per confermare che il messaggio è stato aggiornato. Il valore di esempio riportato sopra viene visualizzato come segue:

   ![changedmessage](assets/changedmessage.png)

>[!NOTE]
>
>La proprietà personalizzata creata potrebbe non essere visualizzata correttamente nella finestra di dialogo Proprietà modulo quando si riapre il modulo. Tuttavia, funziona correttamente e nel modulo viene visualizzato il messaggio Pagina zero aggiornato.
