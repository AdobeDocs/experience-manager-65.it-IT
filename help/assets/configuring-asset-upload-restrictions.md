---
title: Configurare le restrizioni di caricamento delle risorse
description: 'Limitare il tipo di risorse (file) che gli utenti possono caricare '
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Configurare le restrizioni di caricamento delle risorse {#configuring-asset-upload-restrictions}

Puoi configurare Risorse Adobe Experience Manager (AEM) per limitare il tipo di risorse (file) che gli utenti possono caricare. Questa funzione consente di eliminare la possibilità per gli utenti di caricare risorse in un formato indesiderato o qualsiasi file dannoso. Il `Day CQ DAM Asset Upload Restriction` servizio consente di controllare il tipo di file che gli utenti possono caricare. Per impostazione predefinita, AEM Assets consente agli utenti di caricare risorse di tutti i tipi MIME. Tuttavia, potete configurare il servizio per limitare gli utenti al caricamento di file di tipi MIME specifici.

1. Aprite la console Web di Configuration Manager. Accesso `https://[aem_server]:[port]/system/console/configMgr`.
1. Aprite il servizio Limitazione **[!UICONTROL caricamento risorse CQ DAM]** Day in modalità Modifica. Per impostazione predefinita, è selezionata l&#39;opzione **Consenti tutto MIME** , che consente agli utenti di caricare file di tutti i tipi MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Per limitare gli utenti al caricamento di file di alcuni tipi MIME, deselezionate l&#39;opzione **[!UICONTROL Consenti tutti i tipi MIME]** e specificate i tipi MIME consentiti nei campi MIME delle risorse **[!UICONTROL consentite (regex)]** utilizzando espressioni regolari.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Tocca o fai clic su **[!UICONTROL Salva]** per salvare le modifiche. Se specificate stringhe MIME per i tipi MIME consentiti, l&#39;operazione di caricamento non riesce per qualsiasi risorsa con tipo MIME che non corrisponda alle stringhe MIME configurate in questi campi.
