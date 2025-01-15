---
title: Content Services
description: Scopri come utilizzare AEM Mobile Content Services per richiedere contenuti gestiti dall’AEM.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 955ffb1c-4fa9-43bb-8e5b-2df7f2d17951
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 2%

---

# Content Services{#content-services}

{{ue-over-mobile}}

>[!CAUTION]
>
>La funzione Content Services è documentata solo a scopo di anteprima.
>
>È soggetto a modifiche con il rilascio della versione 6.3 Service Pack 1.

AEM Mobile Content Services è una funzione leggera per la richiesta di contenuto gestito dall’AEM. Questo offre a tutti gli sviluppatori di app un modo altamente performante di recuperare i contenuti senza dover avere una conoscenza approfondita dell’archivio dei contenuti (JCR) e del framework web (Sling) dell’AEM. Consente di separare le applicazioni richiedenti dall’archivio dei contenuti.

Content Services introduce diversi nuovi costrutti AEM che consentono a uno sviluppatore di accedere a contenuti gestiti da AEM senza conoscere la struttura dell’archivio di tali contenuti.

Questi costrutti sono necessari per mantenere la flessibilità e consentire l’espansione futura fornendo un livello di astrazione tra i contenuti gestiti dall’AEM e le app mobili che li consumano. Questo consente a AEM Content Services di fungere da livello di astrazione tra i requisiti di contenuto dell&#39;applicazione nativa e l&#39;archivio di contenuti AEM.

Content Services può distribuire il contenuto come risorse, packaged HTML (HTML/CSS/JS) o come contenuto indipendente dal canale.

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
