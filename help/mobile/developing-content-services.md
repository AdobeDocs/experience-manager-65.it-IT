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
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>La funzione Content Services è documentata solo a scopo di anteprima.
>
>È soggetto a modifiche con la versione 6.3 GA Service Pack 1.

AEM Mobile Content Services è una funzionalità leggera per la richiesta di contenuti gestiti da AEM. Questo offre a tutti gli sviluppatori di app un modo altamente performante per recuperare i contenuti senza dover conoscere a fondo AEM archivio di contenuti (JCR) e il framework web (Sling). Consente di scollegare le applicazioni richieste dall’archivio dei contenuti.

Content Services introduce diversi nuovi costrutti AEM che consentono a uno sviluppatore di accedere AEM contenuto gestito senza conoscere la struttura dell’archivio di tale contenuto.

Questi costrutti sono necessari per mantenere la flessibilità e consentire un&#39;espansione futura fornendo un livello di astrazione tra il contenuto gestito AEM e le app mobili che consumano il contenuto. Questo consente a AEM Content Services di funzionare come livello di astrazione tra i requisiti di contenuto dell’applicazione nativa e l’archivio di contenuti AEM.

Content Services può distribuire i contenuti come risorse, pacchetti HTML (HTML/CSS/JS) o come contenuto indipendente dal canale.

>[!CAUTION]
>
>**Prerequisiti:**
>
>Prima di iniziare a utilizzare Content Services, assicurati di abilitare il flag Content Services . Per abilitare la creazione e la gestione di modelli nell’app, devi abilitare i modelli di dati in Browser configurazioni.
>
>Vedi **[Amministrazione dei servizi di contenuti](/help/mobile/developing-content-services.md)** e [Browser di configurazione](/help/sites-administering/configurations.md) documentazione per ulteriori informazioni.

![chlimage_1-143](assets/chlimage_1-143.png)

Dopo aver impostato il flag Content Services e abilitato i modelli di dati nel browser di configurazione, consulta le risorse riportate di seguito per iniziare a utilizzare AEM Mobile Content Services, acquisisci familiarità con i concetti di Content Services come la gestione dei modelli, la gestione delle entità e la distribuzione/rendering dei contenuti per AEM Mobile Content Services.

* Modelli nell’archivio
* Rendering e consegna
