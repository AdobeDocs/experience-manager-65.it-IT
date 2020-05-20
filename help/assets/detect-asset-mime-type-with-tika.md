---
title: Rilevamento del tipo MIME di risorse tramite Apache Tika
description: Abilita Apache Tika per aiutare AEM Assets a rilevare il tipo MIME di risorse dal flusso di contenuto durante l’operazione di caricamento invece che l’estensione del file.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# Detect MIME type of assets using Apache Tika {#detecting-mime-type-of-assets-using-apache-tika}

Normalmente, Risorse Adobe Experience Manager (AEM) rileva il tipo MIME di risorse caricate dall’estensione del file.

Se utilizzate Apache Tika per caricare le risorse, Risorse AEM ne rileva il tipo MIME dal flusso di contenuti durante l’operazione di caricamento invece che dall’estensione del file.

Questa funzione è disattivata per impostazione predefinita. Per abilitare questa funzione, configura il servizio **[!UICONTROL Day CQ DAM Mime Type]** da [!UICONTROL Configuration Manager].

>[!NOTE]
>
>Il rilevamento del tipo MIME con la libreria Apache Tika richiede molte risorse.

1. Per aprire la console Web di Configuration Manager, accedere `https://[aem_server]:[port]/system/console/configMgr`.

1. Dall&#39;elenco dei servizi, individua il servizio **[!UICONTROL Day CQ DAM Mime Type Service]** e fai clic su **[!UICONTROL Modifica]**.

1. Selezionate l’opzione **[!UICONTROL Rileva MIME dal contenuto]** per abilitare l’analisi delle risorse caricate per determinarne il tipo MIME mentre ignorate le estensioni dei file. Per impostazione predefinita, questa opzione è deselezionata.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Click **[!UICONTROL Save]** to save the changes.
