---
title: Rilevamento del tipo MIME di risorse tramite Apache Tika
description: Abilitate Apache Tika per aiutare [!DNL Experience Manager Assets] a rilevare il tipo MIME di risorse dal flusso di contenuto durante l'operazione di caricamento invece che l'estensione del file.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Rilevare il tipo MIME di risorse utilizzando [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

Normalmente, [!DNL Adobe Experience Manager Assets] rileva il tipo MIME di risorse caricate dall&#39;estensione del file.

Se utilizzate [!DNL Apache Tika] per caricare le risorse, [!DNL Assets] ne rileva il tipo MIME dal flusso di contenuto durante l&#39;operazione di caricamento invece dell&#39;estensione del file.

Questa funzione è disattivata per impostazione predefinita. Per abilitare questa funzione, configura il servizio **[!UICONTROL Day CQ DAM Mime Type]** da [!UICONTROL Configuration Manager].

>[!NOTE]
>
>Il rilevamento del tipo MIME con la libreria [!DNL Apache Tika] richiede molte risorse.

1. Per aprire la console Web di Configuration Manager, accedere a `https://[aem_server]:[port]/system/console/configMgr`.

1. Dall&#39;elenco dei servizi, individuare **[!UICONTROL Day CQ DAM Mime Type Service]** e fare clic su **[!UICONTROL Edit]**.

1. Selezionate l&#39;opzione **[!UICONTROL Rileva MIME dal contenuto]** per abilitare l&#39;analisi delle risorse caricate per determinarne il tipo MIME mentre ignorate le estensioni dei file. Per impostazione predefinita, questa opzione è deselezionata.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Fare clic su **[!UICONTROL Salva]** per salvare le modifiche.
