---
title: Configurare le restrizioni di caricamento delle risorse
description: 'Limitare il tipo di risorse (file) che gli utenti possono caricare '
contentOwner: AG
role: Sviluppatore, amministratore, architetto
feature: Gestione risorse,Caricare
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 15%

---


# Configurare le restrizioni di caricamento delle risorse {#configuring-asset-upload-restrictions}

Puoi configurare [!DNL Adobe Experience Manager Assets] per limitare il tipo di risorse che gli utenti possono caricare. Consente di evitare caricamenti accidentali di formati indesiderati e file dannosi. Il servizio `Day CQ DAM Asset Upload Restriction` ti consente di controllare il tipo di file che gli utenti possono caricare. Per impostazione predefinita, [!DNL Assets] consente agli utenti di caricare risorse di tutti i tipi MIME. Tuttavia, puoi configurare il servizio per limitare gli utenti a caricare solo file di tipi MIME specifici.

1. Apri la console Web di Configuration Manager. Accesso `https://[aem_server]:[port]/system/console/configMgr`.
1. Apri il servizio **[!UICONTROL Day CQ DAM Asset Upload Restriction]** in modalità Modifica. Per impostazione predefinita, è selezionata l’opzione **Consenti tutto MIME** , che consente agli utenti di caricare file di tutti i tipi MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Per limitare gli utenti a caricare solo file di determinati tipi MIME, deseleziona l’opzione **[!UICONTROL Consenti tutti i tipi MIME]** e specifica i tipi MIME consentiti nei campi **[!UICONTROL Consentiti MIME (regex)]** utilizzando espressioni regolari.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche. Se specifichi stringhe MIME per i tipi MIME consentiti, l’operazione di caricamento non riuscirà per qualsiasi risorsa il cui tipo MIME non corrisponde alle stringhe MIME configurate in questi campi.
