---
title: Content Services
seo-title: Content Services
description: 'null'
seo-description: 'null'
uuid: 7bd09c91-3931-400b-bdfc-b064b9ca9668
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 6a7e5472-cb57-4c78-b183-7c6dcac11a4e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Content Services{#content-services}

>[!NOTE]
>
>Adobe consiglia di utilizzare SPA Editor per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>La funzione Content Services è documentata solo a scopo di anteprima.
>
>È soggetto a modifiche con il rilascio di 6.3 GA Service Pack 1.

AEM Mobile Content Services è una funzione leggera per richiedere contenuti gestiti da AEM. Questo offre a tutti gli sviluppatori di app un modo altamente performante per recuperare contenuti senza dover conoscere a fondo l&#39;archivio dei contenuti (JCR) di AEM e il framework Web (Sling). Consente di scollegare le applicazioni richieste dall&#39;archivio dei contenuti.

Content Services introduce diversi nuovi costrutti AEM che consentono a uno sviluppatore di accedere al contenuto gestito da AEM senza conoscere la struttura del repository di tale contenuto.

Questi costrutti sono necessari per mantenere la flessibilità e consentire un&#39;espansione futura fornendo un livello di astrazione tra il contenuto gestito da AEM e le app mobili che consumano il contenuto. In questo modo AEM Content Services può fungere da livello di astrazione tra i requisiti di contenuto dell’applicazione nativa e l’archivio dei contenuti di AEM.

Content Services può distribuire i contenuti come risorse, pacchetti HTML (HTML/CSS/JS) o come contenuti indipendenti dai canali.

>[!CAUTION]
>
>**Prerequisiti:**
>
>Prima di iniziare a utilizzare Content Services, assicurati di abilitare il flag Content Services. Per abilitare la creazione e la gestione di modelli nell&#39;app, devi abilitare i modelli di dati nel browser di configurazione.
>
>Per informazioni dettagliate, consultate **[Amministrazione di Content Services](/help/mobile/developing-content-services.md)**.

![chlimage_1-143](assets/chlimage_1-143.png)

Dopo aver impostato il flag Content Services e i modelli di dati attivati nel browser di configurazione, consulta le risorse riportate di seguito per iniziare a utilizzare AEM Mobile Content Services, acquisisci familiarità con i concetti di Content Services come la gestione dei modelli, la gestione delle entità e la distribuzione/rendering dei contenuti per AEM Mobile Content Services.

* Modelli in repository
* Rendering e distribuzione

