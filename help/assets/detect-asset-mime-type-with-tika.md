---
title: Rilevare il tipo MIME di risorse utilizzando Apache Tika
description: Abilita Apache Tika per aiutarti [!DNL Experience Manager Assets] a rilevare il tipo MIME di risorse dal flusso di contenuto durante l'operazione di caricamento anziché l'estensione del file.
contentOwner: AG
role: Admin, Architect
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 1%

---

# Rileva il tipo MIME di risorse utilizzando [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

In genere, [!DNL Adobe Experience Manager Assets] rileva il tipo MIME di risorse caricate dall&#39;estensione del file.

Se utilizzi [!DNL Apache Tika] per caricare le risorse, [!DNL Assets] rileva il tipo MIME dal flusso di contenuto durante l&#39;operazione di caricamento anziché dall&#39;estensione del file.

Questa funzione è disabilitata per impostazione predefinita. Per abilitare la funzionalità, configura il servizio **[!UICONTROL Day CQ DAM Mime Type]** da [!UICONTROL Configuration Manager].

>[!NOTE]
>
>Il rilevamento del tipo MIME tramite la libreria [!DNL Apache Tika] richiede molte risorse.

1. Per aprire la console Web di Configuration Manager, accedere a `https://[aem_server]:[port]/system/console/configMgr`.

1. Dall&#39;elenco dei servizi, individua **[!UICONTROL Day CQ DAM Mime Type Service]** e fai clic su **[!UICONTROL Modifica]**.

1. Seleziona l&#39;opzione **[!UICONTROL Rileva MIME dal contenuto]** per abilitare l&#39;analisi delle risorse caricate per determinarne il tipo MIME ignorando le estensioni dei file. Per impostazione predefinita, questa opzione è deselezionata.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche.
