---
title: Rileva il tipo MIME di risorse utilizzando Apache Tika
description: Abilitare Apache Tika ad aiutare [!DNL Experience Manager Assets] rileva il tipo MIME di risorse dal flusso di contenuto durante l’operazione di caricamento invece dell’estensione del file.
contentOwner: AG
role: Admin, Architect
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Rileva il tipo MIME di risorse utilizzando [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

Normalmente, [!DNL Adobe Experience Manager Assets] rileva il tipo MIME di risorse caricate dalla loro estensione di file.

Se utilizzi [!DNL Apache Tika] per caricare le risorse, [!DNL Assets] rileva il loro tipo MIME dal flusso di contenuto durante l’operazione di caricamento invece dell’estensione del file.

Questa funzione è disabilitata per impostazione predefinita. Per abilitare la funzione, configura la **[!UICONTROL Tipo MIME Day CQ]** servizio da [!UICONTROL Gestione configurazione].

>[!NOTE]
>
>Rilevamento del tipo MIME con [!DNL Apache Tika] libreria è un&#39;operazione ad alta intensità di risorse.

1. Per aprire la console Web di Configuration Manager, accedere a `https://[aem_server]:[port]/system/console/configMgr`.

1. Dall’elenco dei servizi, individua **[!UICONTROL Servizio Day CQ DAM Mime Type]** e fai clic su **[!UICONTROL Modifica]**.

1. Seleziona la **[!UICONTROL Rileva MIME dal contenuto]** per abilitare l’analisi delle risorse caricate per determinare il loro tipo MIME mentre si ignorano le estensioni dei file. Per impostazione predefinita, questa opzione è deselezionata.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche.
