---
title: Rilevamento del tipo MIME di risorse tramite Apache Tika
description: Abilitate Apache Tika per [!DNL Experience Manager Assets] rilevare il tipo MIME di risorse dal flusso di contenuto durante l’operazione di caricamento invece dell’estensione del file.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Rilevamento del tipo MIME di risorse tramite [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

Normalmente, [!DNL Adobe Experience Manager Assets] rileva il tipo MIME delle risorse caricate dall’estensione del file.

Se usate [!DNL Apache Tika] per caricare le risorse, [!DNL Assets] rileva il tipo MIME delle risorse dal flusso di contenuto durante l’operazione di caricamento invece dell’estensione del file.

Questa funzione è disattivata per impostazione predefinita. Per abilitare questa funzione, configura il servizio **[!UICONTROL Day CQ DAM Mime Type]** da [!UICONTROL Configuration Manager].

>[!NOTE]
>
>Il rilevamento del tipo MIME tramite la [!DNL Apache Tika] libreria richiede molte risorse.

1. Per aprire la console Web di Configuration Manager, accedere `https://[aem_server]:[port]/system/console/configMgr`.

1. Dall&#39;elenco dei servizi, individua il servizio **[!UICONTROL Day CQ DAM Mime Type Service]** e fai clic su **[!UICONTROL Modifica]**.

1. Selezionate l’opzione **[!UICONTROL Rileva MIME dal contenuto]** per abilitare l’analisi delle risorse caricate per determinarne il tipo MIME mentre ignorate le estensioni dei file. Per impostazione predefinita, questa opzione è deselezionata.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Click **[!UICONTROL Save]** to save the changes.
