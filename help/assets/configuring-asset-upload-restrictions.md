---
title: Configurare le restrizioni di caricamento delle risorse
description: Limita il tipo di risorse (file) che gli utenti possono caricare
contentOwner: AG
role: Developer, Admin
feature: Asset Management,Upload
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: cda65036-5305-4f01-89da-9b3506ae8c50
    internal-label: Administration
subfeature_v2:
  - id: f1dc0c96-022d-4003-afbe-47bd40173c4a
    internal-label: Upload assets
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 9%
---
# Configurare le restrizioni di caricamento delle risorse {#configuring-asset-upload-restrictions}

È possibile configurare [!DNL Adobe Experience Manager Assets] per limitare il tipo di risorse che gli utenti possono caricare. Aiuta a prevenire caricamenti accidentali di formato indesiderato e file dannosi. Il servizio `Day CQ DAM Asset Upload Restriction` consente di controllare il tipo di file che gli utenti possono caricare. Per impostazione predefinita, [!DNL Assets] consente agli utenti di caricare risorse di tutti i tipi MIME. Tuttavia, puoi configurare il servizio in modo da limitare gli utenti al caricamento solo di file di tipi MIME specifici.

1. Apri la console Web di Configuration Manager. Accedi a `https://[aem_server]:[port]/system/console/configMgr`.
1. Apri il servizio **[!UICONTROL Day CQ DAM Asset Upload Restriction]** in modalità Modifica. Per impostazione predefinita, è selezionata l&#39;opzione **Consenti tutti i tipi MIME**, che consente agli utenti di caricare file di tutti i tipi MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Per limitare gli utenti al caricamento solo di file di determinati tipi MIME, deselezionare l&#39;opzione **[!UICONTROL Consenti tutti i tipi MIME]** e specificare i tipi MIME consentiti nei campi **[!UICONTROL Tipi MIME di risorse consentiti (regex)]** utilizzando espressioni regolari.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche. Se specifichi stringhe MIME per i tipi MIME consentiti, l’operazione di caricamento non riuscirà per qualsiasi risorsa il cui tipo MIME non corrisponde alle stringhe MIME configurate in questi campi.
