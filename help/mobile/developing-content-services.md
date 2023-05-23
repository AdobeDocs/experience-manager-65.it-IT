---
title: Content Services
seo-title: Content Services
description: Content Services
seo-description: null
uuid: 7bd09c91-3931-400b-bdfc-b064b9ca9668
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 6a7e5472-cb57-4c78-b183-7c6dcac11a4e
exl-id: 955ffb1c-4fa9-43bb-8e5b-2df7f2d17951
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 3%

---

# Content Services{#content-services}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>La funzione Content Services è documentata solo a scopo di anteprima.
>
>È soggetta a modifiche con il rilascio della versione 6.3 GA Service Pack 1.

AEM Mobile Content Services è una funzione leggera e leggera per la richiesta di contenuto gestito dall’AEM. Questo offre a tutti gli sviluppatori di app un modo altamente performante di recuperare i contenuti senza dover avere una conoscenza approfondita dell’archivio dei contenuti AEM (JCR) e del framework web (Sling). Consente di separare le applicazioni richiedenti dall’archivio dei contenuti.

Content Services introduce diversi nuovi costrutti AEM che consentono a uno sviluppatore di accedere a contenuti gestiti AEM senza conoscere la struttura dell’archivio di tali contenuti.

Questi costrutti sono necessari per mantenere la flessibilità e consentire l’espansione futura fornendo un livello di astrazione tra il contenuto gestito dall’AEM e le app mobili che lo utilizzano. Questo consente a AEM Content Services di funzionare come livello di astrazione tra i requisiti di contenuto dell’applicazione nativa e l’archivio di contenuti AEM.

Content Services può distribuire il contenuto come risorse, packaged HTML (HTML/CSS/JS) o come contenuto indipendente dal canale.

>[!CAUTION]
>
>**Prerequisiti:**
>
>Prima di iniziare a utilizzare Content Services, assicurati di abilitare il flag Content Services. Per abilitare la creazione e la gestione dei modelli nell’app, devi abilitare i modelli di dati nel browser configurazioni.
>
>Consulta **[Amministrazione di Content Services](/help/mobile/developing-content-services.md)** e [Browser configurazioni](/help/sites-administering/configurations.md) per ulteriori informazioni.

![chlimage_1-143](assets/chlimage_1-143.png)

Dopo aver impostato il flag Content Services e abilitato i modelli dati nel browser configurazioni, consulta le risorse riportate di seguito per iniziare a utilizzare AEM Mobile Content Services, conoscere i concetti di Content Services, ad esempio gestione dei modelli e delle entità, seguiti dalla distribuzione/rendering dei contenuti per AEM Mobile Content Services.

* Modelli nell’archivio
* Rendering e consegna
