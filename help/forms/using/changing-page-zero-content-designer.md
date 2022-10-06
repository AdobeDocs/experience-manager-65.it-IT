---
title: Modifica del contenuto della pagina Zero in Designer
seo-title: Changing Page Zero content in Designer
description: Sai come modificare il messaggio visualizzato sulla pagina Zero di un PDF XFA quando lo visualizzi in un visualizzatore non Adobe PDF?
seo-description: Do you know how you can change the message displayed on Page Zero of an XFA PDF when viewing it in a non-Adobe PDF viewer?
uuid: ac23fb21-3f15-48ea-aeeb-4ecc12b771ac
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 56b6a573-8aba-43e7-acb7-c2da45869d95
docset: aem65
feature: Adaptive Forms
exl-id: 466b7e85-a2f8-4e1e-8afc-1566b0ccb84c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# Modifica del contenuto della pagina Zero in Designer {#changing-page-zero-content-in-designer}

Il contenuto della pagina Zero viene visualizzato per impostazione predefinita quando un visualizzatore non Adobe PDF, ad esempio il visualizzatore PDF predefinito in [!DNL Chrome] o [!DNL Firefox], non è in grado di leggere il contenuto del modulo PDF/XFA. Il messaggio predefinito Zero pagina è mostrato di seguito.

![defaultpage0message](assets/defaultpage0message.png)

[!DNL AEM Forms] La versione di Designer consente di modificare il messaggio visualizzato sulla pagina Zero. Per modificare il messaggio Zero pagina, esegui le seguenti operazioni:

1. Assicurati di disporre della [!DNL AEM Forms] versione di Designer installata. È possibile controllare la versione dalla schermata Informazioni su di designer.

1. Aprire il modulo per il quale si desidera modificare il contenuto Zero pagina.

1. Fai clic su **[!UICONTROL File]** > **[!UICONTROL Proprietà modulo]**.

1. In [!UICONTROL Proprietà modulo] finestra di dialogo, fai clic su ![plus](assets/plus.png) (Icona Plus) per aggiungere una proprietà personalizzata.

1. Specifica **_pagezerocontent** come nome della proprietà.
1. Aggiungi come valore il nuovo messaggio Zero pagina in formato RTF. Esempio:


   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. Salvare il modulo come PDF.

1. Visualizza il modulo PDF nel browser per confermare l’aggiornamento del messaggio. Il valore di esempio sopra viene visualizzato come segue:

   ![changedmessage](assets/changedmessage.png)

>[!NOTE]
>
>La proprietà personalizzata appena creata potrebbe non essere visualizzata correttamente nella finestra di dialogo Proprietà modulo quando si riapre il modulo. Tuttavia, funziona correttamente e nel modulo viene visualizzato il messaggio Zero pagina aggiornato.
