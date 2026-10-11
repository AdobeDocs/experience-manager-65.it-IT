---
title: Content Services
description: Scopri come utilizzare AEM Mobile Content Services per richiedere contenuti gestiti da AEM.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 955ffb1c-4fa9-43bb-8e5b-2df7f2d17951
solution: Experience Manager
feature: Mobile
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 2%
---
# Content Services{#content-services}

{{ue-over-mobile}}

>[!CAUTION]
>
>La funzione Content Services è documentata solo a scopo di anteprima.
>
>È soggetto a modifiche con il rilascio della versione 6.3 Service Pack 1.

AEM Mobile Content Services è una funzione leggera per la richiesta di contenuti gestiti da AEM. Questo offre a tutti gli sviluppatori di app un modo altamente performante di recuperare i contenuti senza dover avere una conoscenza approfondita dell’archivio dei contenuti (JCR) e del framework web (Sling) di AEM. Consente di separare le applicazioni richiedenti dall’archivio dei contenuti.

Content Services introduce diversi nuovi costrutti AEM che consentono a uno sviluppatore di accedere a contenuti gestiti da AEM senza conoscere la struttura dell’archivio di tali contenuti.

Questi costrutti sono necessari per mantenere la flessibilità e consentire l’espansione futura fornendo un livello di astrazione tra il contenuto gestito da AEM e le app mobili che lo utilizzano. Questo consente ad AEM Content Services di funzionare come livello di astrazione tra i requisiti di contenuto dell’applicazione nativa e l’archivio dei contenuti di AEM.

Content Services può distribuire i contenuti come risorse, HTML in pacchetto (HTML/CSS/JS) o come contenuti indipendenti dal canale.

>[!CAUTION]
>
>**Prerequisiti:**
>
>Prima di iniziare a utilizzare Content Services, assicurati di abilitare il flag Content Services. Per abilitare la creazione e la gestione dei modelli nell’app, abilita i modelli di dati nel browser configurazioni.
>
>Per ulteriori informazioni, vedere **[Amministrazione di Content Services](/help/mobile/developing-content-services.md)** e la documentazione di [Browser configurazioni](/help/sites-administering/configurations.md).

![chlimage_1-143](assets/chlimage_1-143.png)

Dopo aver impostato il flag Content Services e abilitato i modelli dati nel Browser configurazioni, consulta le risorse di seguito per iniziare a utilizzare AEM Mobile Content Services. Acquisisci familiarità con i concetti di Content Services, ad esempio gestione dei modelli e delle entità, seguiti dalla distribuzione/rendering dei contenuti per AEM Mobile Content Services.

* Modelli nell’archivio
* Rendering e consegna
