---
title: Configurare le restrizioni di caricamento delle risorse
description: Limitare il tipo di risorse (file) che gli utenti possono caricare
contentOwner: AG
role: Developer, Admin, Architect
feature: Asset Management,Upload
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 20%

---

# Configurare le restrizioni di caricamento delle risorse {#configuring-asset-upload-restrictions}

Puoi configurare [!DNL Adobe Experience Manager Assets] per limitare il tipo di risorse che gli utenti possono caricare. Consente di evitare caricamenti accidentali di formati indesiderati e file dannosi. La `Day CQ DAM Asset Upload Restriction` consente di controllare il tipo di file che gli utenti possono caricare. Per impostazione predefinita, [!DNL Assets] consente agli utenti di caricare risorse di tutti i tipi MIME. Tuttavia, puoi configurare il servizio per limitare gli utenti a caricare solo file di tipi MIME specifici.

1. Apri la console Web di Configuration Manager. Accesso `https://[aem_server]:[port]/system/console/configMgr`.
1. Apri **[!UICONTROL Restrizione al caricamento delle risorse DAM del giorno CQ]** in modalità Modifica. Per impostazione predefinita, la **Consenti tutto** , che consente agli utenti di caricare file di tutti i tipi MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Per limitare gli utenti a caricare solo file di determinati tipi MIME, deseleziona **[!UICONTROL Consenti tutto]** e specifica i tipi MIME consentiti nel **[!UICONTROL MIME consentiti (regex)]** campi che utilizzano espressioni regolari.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche. Se specifichi stringhe MIME per i tipi MIME consentiti, l’operazione di caricamento non riuscirà per qualsiasi risorsa il cui tipo MIME non corrisponde alle stringhe MIME configurate in questi campi.
