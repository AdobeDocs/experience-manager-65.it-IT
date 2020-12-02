---
title: Content Services
seo-title: Servizi contenuto
description: 'null'
seo-description: 'null'
uuid: 7bd09c91-3931-400b-bdfc-b064b9ca9668
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 6a7e5472-cb57-4c78-b183-7c6dcac11a4e
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 3%

---


# Content Services{#content-services}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>La funzione Content Services è documentata solo a scopo di anteprima.
>
>È soggetto a modifiche con il rilascio di 6.3 GA Service Pack 1.

 AEM Mobile Content Services è una funzionalità leggera per la richiesta di contenuti gestiti da AEM. Questo fornisce a tutti gli sviluppatori di app un modo altamente performante per recuperare il contenuto senza dover conoscere a fondo AEM repository dei contenuti (JCR) e il framework Web (Sling). Consente di scollegare le applicazioni richieste dall&#39;archivio dei contenuti.

Content Services introduce diversi nuovi costrutti AEM che consentono a uno sviluppatore di accedere AEM contenuto gestito senza conoscere la struttura del repository di tale contenuto.

Questi costrutti sono necessari per mantenere la flessibilità e consentire l&#39;espansione futura fornendo un livello di astrazione tra il contenuto gestito AEM e le app mobili che consumano il contenuto. In questo modo AEM Content Services può fungere da livello di astrazione tra i requisiti di contenuto dell&#39;applicazione nativa e l&#39;archivio dei contenuti AEM.

Content Services può distribuire i contenuti come risorse, pacchetti HTML (HTML/CSS/JS) o come contenuti indipendenti dai canali.

>[!CAUTION]
>
>**Prerequisiti:**
>
>Prima di iniziare a utilizzare Content Services, assicurati di abilitare il flag Content Services. Per abilitare la creazione e la gestione di modelli nell&#39;app, devi abilitare i modelli di dati nel browser di configurazione.
>
>Per ulteriori informazioni, vedere **[Amministrazione di Content Services](/help/mobile/developing-content-services.md)** e la documentazione del [browser di configurazione](/help/sites-administering/configurations.md).

![chlimage_1-143](assets/chlimage_1-143.png)

Dopo aver impostato il flag Content Services e i modelli di dati abilitati nel browser di configurazione, consulta le risorse riportate di seguito per iniziare a utilizzare  AEM Mobile Content Services, per acquisire familiarità con i concetti di Content Services come la gestione dei modelli, la gestione delle entità e la distribuzione/rendering dei contenuti per  AEM Mobile Content Services.

* Modelli nell&#39;archivio
* Rendering e distribuzione
