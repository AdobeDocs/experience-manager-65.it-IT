---
title: Rileva il tipo MIME di risorse utilizzando Apache Tika
description: Abilita Apache Tika per aiutare [!DNL Experience Manager Assets] a rilevare il tipo MIME di risorse dal flusso di contenuto durante l'operazione di caricamento invece dell'estensione del file.
contentOwner: AG
role: Amministratore, architetto
feature: Metadati, Strumenti per sviluppatori, Gestione risorse
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# Rileva il tipo MIME di risorse utilizzando [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

Normalmente, [!DNL Adobe Experience Manager Assets] rileva il tipo MIME di risorse caricate dalla loro estensione di file.

Se utilizzi [!DNL Apache Tika] per caricare le risorse, [!DNL Assets] rileva il loro tipo MIME dal flusso di contenuto durante l’operazione di caricamento anziché dall’estensione del file.

Questa funzione è disabilitata per impostazione predefinita. Per abilitare la funzione, configura il servizio **[!UICONTROL Day CQ DAM Mime Type]** da [!UICONTROL Configuration Manager].

>[!NOTE]
>
>Il rilevamento del tipo MIME con la libreria [!DNL Apache Tika] è un’operazione ad alta intensità di risorse.

1. Per aprire la console Web di Configuration Manager, accedi a `https://[aem_server]:[port]/system/console/configMgr`.

1. Dall&#39;elenco dei servizi, individua **[!UICONTROL Day CQ DAM Mime Type Service]** e fai clic su **[!UICONTROL Modifica]**.

1. Seleziona l’opzione **[!UICONTROL Rileva MIME dal contenuto]** per abilitare l’analisi delle risorse caricate per determinarne il tipo MIME mentre ignora le estensioni dei file. Per impostazione predefinita, questa opzione è deselezionata.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche.
