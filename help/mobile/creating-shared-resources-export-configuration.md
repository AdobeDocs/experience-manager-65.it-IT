---
title: Creazione della configurazione di esportazione delle risorse condivise
seo-title: Creating Shared Resources Export Configuration
description: Segui questa pagina per informazioni sull’esportazione di risorse condivise da Adobe Experience Manager (AEM) per il caricamento in AEM Mobile.
seo-description: Follow this page to learn about exporting shared resources from Adobe Experience Manager (AEM) for upload to AEM Mobile.
uuid: 99b8ff94-8135-4643-a15b-aa6fb91f5401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 1edf6c76-ccb1-40b6-bdf6-924f1461cd28
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 1%

---

# Creazione della configurazione di esportazione delle risorse condivise{#creating-shared-resources-export-configuration}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**Prerequisito**:
>
>Prima di scoprire come creare e modificare risorse condivise, consulta [Sincronizzazione dei contenuti](/help/mobile/mobile-ondemand-contentsync.md) per comprendere i concetti di base.

Gli utenti di AEM Mobile utilizzano Content Sync per esportare i contenuti live in contenuti statici da utilizzare nelle app mobili e questa esportazione si verifica quando il contenuto viene caricato su Mobile On-Demand Services da AEM Mobile.

La proprietà ***dps-exportTemplate*** indicato nella tabella precedente, definisce il percorso delle configurazioni di esportazione dell’app. Imposta questa proprietà per creare e modificare le risorse condivise.

Le risorse seguenti descrivono l’esportazione di risorse condivise da Adobe Experience Manager (AEM) per il caricamento in AEM Mobile.

Risorse condivise di HTML consente agli articoli di condividere risorse di HTML che altrimenti avrebbero bisogno di essere duplicate per tutti gli articoli e possono includere icone, font, javascript e css.

Configurazione della sincronizzazione dei contenuti trovata in **&lt;dps-exporttemplate>/dps-HTMLResource>** deve essere configurato per esportare tutto il contenuto di un articolo richiesto per il rendering statico delle proprietà sul dispositivo.

>[!CAUTION]
>
>Puoi eseguire i passaggi seguenti per visualizzare le risorse condivise di esempio, solo se disponi di:
>
>* è stato installato il contenuto di esempio
>* esecuzione AEM&#39;istanza
>* nessun contesto personalizzato configurato o una porta diversa
>


Per visualizzare un esempio di risorsa condivisa, vedi i passaggi seguenti:

1. Apri CRXDE Lite sul server AEM.
1. Sfoglia questo percorso *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResource](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*, per visualizzare le risorse condivise di esempio.

   Puoi visualizzare tutte le proprietà necessarie per la creazione delle risorse condivise, come illustrato nella figura seguente:

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>Le risorse condivise devono essere caricate o esportate in AEM Mobile On-demand Services quando una qualsiasi delle risorse condivise cambia.
