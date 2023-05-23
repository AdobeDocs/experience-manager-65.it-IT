---
title: Configurare le restrizioni di caricamento delle risorse
description: Limita il tipo di risorse (file) che gli utenti possono caricare
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

Puoi configurare [!DNL Adobe Experience Manager Assets] per limitare il tipo di risorse che gli utenti possono caricare. Aiuta a prevenire caricamenti accidentali di formato indesiderato e file dannosi. Il `Day CQ DAM Asset Upload Restriction` consente di controllare il tipo di file che gli utenti possono caricare. Per impostazione predefinita, [!DNL Assets] consente agli utenti di caricare risorse di tutti i tipi MIME. Tuttavia, puoi configurare il servizio in modo da limitare gli utenti al caricamento solo di file di tipi MIME specifici.

1. Apri la console Web di Configuration Manager. Accesso `https://[aem_server]:[port]/system/console/configMgr`.
1. Apri **[!UICONTROL Limitazione caricamento risorse DAM Day CQ]** in modalità Modifica. Per impostazione predefinita, il **Consenti tutti MIME** è selezionata, che consente agli utenti di caricare file di tutti i tipi MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Per limitare gli utenti al caricamento solo di file di determinati tipi MIME, deseleziona la **[!UICONTROL Consenti tutti MIME]** e specificare i tipi MIME consentiti nella **[!UICONTROL MIME risorse consentite (regex)]** campi utilizzando espressioni regolari.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Clic **[!UICONTROL Salva]** per salvare le modifiche. Se specifichi stringhe MIME per i tipi MIME consentiti, l’operazione di caricamento non riuscirà per qualsiasi risorsa il cui tipo MIME non corrisponde alle stringhe MIME configurate in questi campi.
