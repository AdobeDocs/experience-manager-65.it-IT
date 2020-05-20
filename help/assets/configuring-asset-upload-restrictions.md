---
title: Configurare le restrizioni di caricamento delle risorse
description: 'Limitare il tipo di risorse (file) che gli utenti possono caricare '
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 15%

---


# Configurare le restrizioni di caricamento delle risorse {#configuring-asset-upload-restrictions}

Potete configurare [!DNL Adobe Experience Manager Assets] per limitare il tipo di risorse che gli utenti possono caricare. Consente di evitare caricamenti accidentali di formati indesiderati e file dannosi. Il `Day CQ DAM Asset Upload Restriction` servizio consente di controllare il tipo di file che gli utenti possono caricare. Per impostazione predefinita, [!DNL Assets] consente agli utenti di caricare risorse di tutti i tipi MIME. Tuttavia, potete configurare il servizio per limitare gli utenti al caricamento di file di tipi MIME specifici.

1. Aprite la console Web di Configuration Manager. Accesso `https://[aem_server]:[port]/system/console/configMgr`.
1. Aprite il servizio Limitazione **[!UICONTROL caricamento risorse CQ DAM]** Day in modalità Modifica. Per impostazione predefinita, è selezionata l&#39;opzione **Consenti tutto MIME** , che consente agli utenti di caricare file di tutti i tipi MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. To restrict users to upload files of certain MIME types only, unselect the **[!UICONTROL Allow all MIME]** option and specify allowed MIME types in the **[!UICONTROL Allowed Asset MIMEs (regex)]** fields using regular expressions.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Click **[!UICONTROL Save]** to save the changes. Se specifichi stringhe MIME per i tipi MIME consentiti, l’operazione di caricamento non riuscirà per qualsiasi risorsa il cui tipo MIME non corrisponde alle stringhe MIME configurate in questi campi.
