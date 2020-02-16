---
title: Creazione della configurazione di esportazione delle risorse condivise
seo-title: Creazione della configurazione di esportazione delle risorse condivise
description: Seguite questa pagina per informazioni sull'esportazione di risorse condivise da Adobe Experience Manager (AEM) per il caricamento in AEM Mobile.
seo-description: Seguite questa pagina per informazioni sull'esportazione di risorse condivise da Adobe Experience Manager (AEM) per il caricamento in AEM Mobile.
uuid: 99b8ff94-8135-4643-a15b-aa6fb91f5401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 1edf6c76-ccb1-40b6-bdf6-924f1461cd28
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Creazione della configurazione di esportazione delle risorse condivise{#creating-shared-resources-export-configuration}

>[!NOTE]
>
>Adobe consiglia di utilizzare SPA Editor per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**Prerequisito**:
>
>Prima di apprendere come creare e modificare risorse condivise, consultate Sincronizzazione [dei](/help/mobile/mobile-ondemand-contentsync.md) contenuti per comprendere i concetti di base.

Gli utenti di AEM Mobile utilizzano la sincronizzazione dei contenuti per esportare contenuti live in contenuti statici da utilizzare nelle app mobili. Questa esportazione si verifica quando il contenuto viene caricato nei servizi on-demand Mobile da AEM Mobile.

La proprietà ***dps-exportTemplate*** citata nella tabella precedente definisce il percorso delle configurazioni di esportazione dell&#39;app. Impostate questa proprietà per creare e modificare le risorse condivise.

Le risorse seguenti descrivono l&#39;esportazione di risorse condivise da Adobe Experience Manager (AEM) per il caricamento in AEM Mobile.

Risorse HTML condivise consente agli articoli di condividere risorse HTML che altrimenti avrebbero bisogno di essere duplicate per tutti gli articoli e che possono includere icone, font, javascript e css.

La configurazione di sincronizzazione dei contenuti trovata in **&lt;dps-exportTemplate>/dps-HTMLResources>** deve essere configurata per esportare tutto il contenuto un articolo richiesto per il rendering statico delle proprietà sul dispositivo.

>[!CAUTION]
>
>Per visualizzare le risorse condivise di esempio, potete eseguire le operazioni seguenti solo se:
>
>* installato il contenuto di esempio
>* esecuzione di un’istanza AEM
>* nessun contesto personalizzato configurato o porta diversa
>



Per visualizzare un esempio di risorsa condivisa, procedere come segue:

1. Apri CRXDE Lite sul server AEM.
1. Andate a questo percorso *[/etc/contentsync/templates/dps-we-illimitato-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*per visualizzare le risorse condivise di esempio.

   Potete visualizzare tutte le proprietà necessarie per creare le risorse condivise come illustrato nella figura seguente:

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>Le risorse condivise devono essere caricate o esportate in AEM Mobile On-Demand Services quando una delle risorse condivise cambia.

