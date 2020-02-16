---
title: Rilevamento del tipo MIME di risorse tramite Apache Tika
description: Abilita Apache Tika per aiutare AEM Assets a rilevare il tipo MIME di risorse dal flusso di contenuto durante l’operazione di caricamento invece che l’estensione del file.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Detect MIME type of assets using Apache Tika {#detecting-mime-type-of-assets-using-apache-tika}

Normalmente, Risorse Adobe Experience Manager (AEM) rileva il tipo MIME di risorse caricate dall’estensione del file.

Se utilizzate Apache Tika per caricare le risorse, Risorse AEM ne rileva il tipo MIME dal flusso di contenuti durante l’operazione di caricamento invece che dall’estensione del file.

Questa funzione è disattivata per impostazione predefinita. Per abilitare questa funzione, configura il servizio **[!UICONTROL Day CQ DAM Mime Type]** da [!UICONTROL Configuration Manager].

>[!NOTE]
>
>Il rilevamento del tipo MIME tramite la libreria Apache Tika richiede molte risorse.

1. Per aprire la console Web di Configuration Manager, accedere `https://[aem_server]:[port]/system/console/configMgr`.
1. Dall’elenco dei servizi, individua il servizio **[!UICONTROL Day CQ DAM Mime Type Service]** e tocca **[!UICONTROL Modifica]** accanto a esso per aprirlo in modalità di modifica.

1. Selezionate l’opzione **[!UICONTROL Rileva MIME dal contenuto]** per abilitare l’analisi delle risorse caricate per determinarne il tipo MIME mentre ignorate le estensioni dei file. Per impostazione predefinita, questa opzione è deselezionata.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Tocca o fai clic su **[!UICONTROL Salva]** per salvare le modifiche.
