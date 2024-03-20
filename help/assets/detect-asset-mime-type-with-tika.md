---
title: Rilevare il tipo MIME di risorse utilizzando Apache Tika
description: Abilita Apache Tika per aiutarti [!DNL Experience Manager Assets] rileva il tipo MIME di risorse dal flusso di contenuto durante l’operazione di caricamento anziché dall’estensione del file.
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

# Rileva il tipo MIME di risorse tramite [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

Normalmente, [!DNL Adobe Experience Manager Assets] rileva il tipo MIME delle risorse caricate dall’estensione del file.

Se usa [!DNL Apache Tika] per caricare le risorse, [!DNL Assets] rileva il tipo MIME dal flusso di contenuto durante l’operazione di caricamento anziché dall’estensione del file.

Questa funzione è disabilitata per impostazione predefinita. Per abilitare la funzione, configura **[!UICONTROL Tipo MIME DAM Day CQ]** servizio da [!UICONTROL Gestione configurazione].

>[!NOTE]
>
>Rilevamento del tipo MIME tramite [!DNL Apache Tika] la libreria è un&#39;operazione che richiede molte risorse.

1. Per aprire la console Web di Configuration Manager, accedere `https://[aem_server]:[port]/system/console/configMgr`.

1. Dall’elenco dei servizi, individua **[!UICONTROL Servizio Day CQ DAM Mime Type]** e fai clic su **[!UICONTROL Modifica]**.

1. Seleziona la **[!UICONTROL Rileva MIME dal contenuto]** per abilitare l’analisi delle risorse caricate per determinarne il tipo MIME, ignorando le estensioni dei file. Per impostazione predefinita, questa opzione è deselezionata.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Clic **[!UICONTROL Salva]** per salvare le modifiche.
