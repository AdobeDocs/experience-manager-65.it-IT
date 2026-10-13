---
title: Rilevare il tipo di risorse MIME utilizzando Apache Tika
description: Abilita Apache Tika per aiutare [!DNL Experience Manager Assets] a rilevare il tipo MIME di risorse dal flusso di contenuto durante l'operazione di caricamento anziché l'estensione del file.
contentOwner: AG
role: Admin, Developer
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: ed6971a3-2c12-4fd2-81f4-ff329c416250
    internal-label: Metadata
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 9%
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
