---
title: Modifica del contenuto di Page Zero in Designer
seo-title: Changing Page Zero content in Designer
description: Sapete come modificare il messaggio visualizzato sulla pagina zero di un PDF XFA quando lo si visualizza in un visualizzatore non Adobe PDF?
seo-description: Do you know how you can change the message displayed on Page Zero of an XFA PDF when viewing it in a non-Adobe PDF viewer?
uuid: ac23fb21-3f15-48ea-aeeb-4ecc12b771ac
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 56b6a573-8aba-43e7-acb7-c2da45869d95
docset: aem65
feature: Adaptive Forms
exl-id: 466b7e85-a2f8-4e1e-8afc-1566b0ccb84c
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 1%

---

# Modifica del contenuto di Page Zero in Designer {#changing-page-zero-content-in-designer}

Il contenuto Pagina zero viene visualizzato per impostazione predefinita quando un visualizzatore non Adobe PDF, ad esempio il visualizzatore PDF predefinito in [!DNL Chrome] o [!DNL Firefox], non può leggere il contenuto del modulo PDF/XFA. Di seguito viene visualizzato il messaggio predefinito Pagina zero.

![defaultpage0message](assets/defaultpage0message.png)

[!DNL AEM Forms] versione di Designer consente di modificare il messaggio visualizzato nella pagina zero. Per modificare il messaggio Pagina zero, effettuare le seguenti operazioni:

1. Assicurati di disporre di [!DNL AEM Forms] versione di Designer installata. Puoi controllare la versione dalla schermata Informazioni su di Designer.

1. Aprire il modulo di cui si desidera modificare il contenuto Pagina zero.

1. Clic **[!UICONTROL File]** > **[!UICONTROL Proprietà modulo]**.

1. In [!UICONTROL Proprietà modulo] , fai clic su ![più](assets/plus.png) (Icona Più) per aggiungere una proprietà personalizzata.

1. Specifica **_pagezerocontent** come nome della proprietà.
1. Aggiungi come valore il nuovo messaggio Pagina zero, in formato Testo formattato. Ad esempio:


   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. Salvare il modulo come PDF.

1. Visualizza il modulo PDF nel browser per confermare che il messaggio è stato aggiornato. Il valore di esempio riportato sopra viene visualizzato come segue:

   ![changedmessage](assets/changedmessage.png)

>[!NOTE]
>
>La proprietà personalizzata appena creata potrebbe non essere visualizzata correttamente nella finestra di dialogo Proprietà maschera quando si riapre la maschera. Tuttavia, funziona correttamente e nel modulo viene visualizzato il messaggio Pagina zero aggiornato.
