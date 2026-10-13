---
title: Risorsa multilingue
description: Scopri come automatizzare i flussi di lavoro per tradurre le risorse, inclusi file binari, metadati e tag, in più lingue.
contentOwner: AG
feature: Asset Management
role: Admin
exl-id: edccf23c-087e-4253-babb-dd4c6610517d
hide: true
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 15%
---
# Risorse multilinguistiche {#multilingual-assets}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/translate-assets.html?lang=it) |
| AEM 6.5 | Questo articolo |

[!DNL Adobe Experience Manager Assets] consente di automatizzare i flussi di lavoro di traduzione delle risorse (inclusi file binari, metadati e tag) per generare risorse in altre lingue da utilizzare nei progetti multilingue.

Per automatizzare i flussi di lavoro di traduzione, è necessario integrare i fornitori di servizi di traduzione con [!DNL Experience Manager] e creare progetti per la traduzione delle risorse in più lingue. [!DNL Experience Manager] supporta flussi di lavoro di traduzione umana e automatica.

Traduzione umana: le risorse tradotte vengono restituite e importate in [!DNL Experience Manager]. Quando il provider di traduzione è integrato con [!DNL Experience Manager], le risorse vengono inviate automaticamente tra [!DNL Experience Manager] e il provider di traduzione.

Traduzione automatica: il servizio di traduzione automatica traduce immediatamente i metadati e i tag per le risorse.

La traduzione delle risorse include quanto segue:

1. [Connettere Experience Manager al fornitore di servizi di traduzione](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [Creare configurazioni del framework di integrazione della traduzione](/help/sites-administering/tc-tic.md)
1. [Preparare le risorse per la traduzione](preparing-assets-for-translation.md)
1. [Applicare i servizi cloud di traduzione alle cartelle](transition-cloud-services.md)
1. [Creare progetti di traduzione](translation-projects.md)

Se il provider di servizi di traduzione non fornisce un connettore da integrare con [!DNL Experience Manager], utilizzare un [processo alternativo](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Vedi anche [Creare progetti di traduzione per frammenti di contenuto](creating-translation-projects-for-content-fragments.md).
