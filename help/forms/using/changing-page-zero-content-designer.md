---
title: Modifica del contenuto Page Zero in Designer
seo-title: Modifica del contenuto Page Zero in Designer
description: Sapete come modificare il messaggio visualizzato sulla pagina Zero di un PDF XFA quando lo visualizzate in un visualizzatore Adobe PDF non ?
seo-description: Sapete come modificare il messaggio visualizzato sulla pagina Zero di un PDF XFA quando lo visualizzate in un visualizzatore Adobe PDF non ?
uuid: ac23fb21-3f15-48ea-aeeb-4ecc12b771ac
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 56b6a573-8aba-43e7-acb7-c2da45869d95
docset: aem65
translation-type: tm+mt
source-git-commit: 3cbcd23254e16231a199276aa2f9e70d6ff39b34
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---


# Modifica del contenuto Page Zero in Designer {#changing-page-zero-content-in-designer}

Il contenuto della pagina Zero è visualizzato per impostazione predefinita quando un visualizzatore Adobe PDF non , ad esempio il visualizzatore PDF predefinito in [!DNL Chrome] o [!DNL Firefox], non è in grado di leggere il contenuto del modulo PDF/XFA. Il messaggio predefinito Page Zero è riportato di seguito.

![defaultpage0message](assets/defaultpage0message.png)

[!DNL AEM Forms] la versione di Designer consente di modificare il messaggio visualizzato sulla pagina Zero. Per modificare il messaggio Page Zero, effettuare le seguenti operazioni:

1. Verificare che sia installata la [!DNL AEM Forms] versione di Designer. È possibile controllare la versione dalla schermata Informazioni su di Designer.

1. Aprire il modulo per il quale si desidera modificare il contenuto Page Zero.

1. Click **[!UICONTROL File]** > **[!UICONTROL Form Properties]**.

1. Nella finestra di dialogo Proprietà  modulo, fare clic su ![più](assets/plus.png) (icona più) per aggiungere una proprietà personalizzata.

1. Specificate **_pagezerocontent** come nome della proprietà.
1. Aggiungete il nuovo messaggio Page Zero, in formato RTF, come valore. Esempio:


   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. Salvare il modulo come PDF.

1. Visualizzare il modulo PDF nel browser per confermare l&#39;aggiornamento del messaggio. Il valore di esempio sopra viene visualizzato come segue:

   ![changedmessage](assets/changedmessage.png)

>[!NOTE]
>
>La proprietà personalizzata appena creata potrebbe non essere visualizzata correttamente nella finestra di dialogo Proprietà modulo quando si riapre il modulo. Tuttavia, funziona correttamente e il modulo visualizza il messaggio Page Zero aggiornato.
