---
title: Creazione configurazione esportazione risorse condivise
seo-title: Creating Shared Resources Export Configuration
description: Segui questa pagina per scoprire come esportare risorse condivise da Adobe Experience Manager (AEM) per caricarle in AEM Mobile.
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

# Creazione configurazione esportazione risorse condivise{#creating-shared-resources-export-configuration}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**Prerequisito**:
>
>Prima di scoprire come creare e modificare le risorse condivise, consulta [Sincronizzazione contenuti](/help/mobile/mobile-ondemand-contentsync.md) per comprendere i concetti di base.

Gli utenti di AEM Mobile utilizzano Sincronizzazione contenuti per esportare contenuti live in contenuti statici da utilizzare nelle app mobili. Questa esportazione si verifica quando i contenuti vengono caricati in Mobile On-Demand Services da AEM Mobile.

La proprietà ***dps-exportTemplate*** indicato nella tabella precedente, definisce il percorso delle configurazioni di esportazione dell’app. Impostare questa proprietà per creare e modificare le risorse condivise.

Le risorse seguenti descrivono l’esportazione di risorse condivise da Adobe Experience Manager (AEM) per il caricamento in AEM Mobile.

Le risorse HTML condivise consentono agli articoli di condividere risorse HTML che altrimenti dovrebbero essere duplicate per tutti gli articoli e che possono includere icone, font, JavaScript e CSS.

La configurazione di Sincronizzazione contenuti trovata in **&lt;dps-exporttemplate>/dps-HTMLResources>** deve essere configurato per esportare tutto il contenuto di un articolo necessario per il rendering statico della proprietà sul dispositivo.

>[!CAUTION]
>
>Puoi eseguire i passaggi seguenti per visualizzare risorse condivise di esempio, solo se:
>
>* ha installato il contenuto di esempio
>* esecuzione dell’istanza AEM
>* nessun contesto personalizzato configurato o una porta diversa
>


Per visualizzare un esempio di risorsa condivisa, consulta i passaggi seguenti:

1. Apri CRXDE Lite sul server AEM.
1. Passa a questo percorso *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*, per visualizzare le risorse condivise di esempio.

   Puoi visualizzare tutte le proprietà necessarie per creare le risorse condivise, come illustrato nella figura seguente:

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>Le risorse condivise devono essere caricate o esportate in AEM Mobile On-demand Services quando una qualsiasi delle risorse condivise cambia.
