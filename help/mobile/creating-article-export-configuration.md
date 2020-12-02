---
title: Creazione della configurazione di esportazione degli articoli
seo-title: Creazione della configurazione di esportazione degli articoli
description: Seguite questa pagina per informazioni sull’esportazione di contenuti da Adobe Experience Manager (AEM) per il caricamento  AEM Mobile.
seo-description: Seguite questa pagina per informazioni sull’esportazione di contenuti da Adobe Experience Manager (AEM) per il caricamento  AEM Mobile.
uuid: 089bc15b-669e-4623-bdbb-fd9abf46e098
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: bc681589-5d46-44cd-888d-b0722a2fd006
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---


# Creazione della configurazione dell&#39;esportazione di articoli{#creating-article-export-configuration}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**Prerequisito**:
>
>Prima di apprendere come creare e modificare le risorse condivise, consultate [Content Sync](/help/mobile/mobile-ondemand-contentsync.md) per comprendere i concetti di base.

 utenti AEM Mobile utilizzano Content Sync per esportare contenuti live in contenuti statici da utilizzare nelle app mobili. Questa esportazione si verifica quando il contenuto viene caricato nei servizi on-demand Mobile da  AEM Mobile.

La proprietà ***dps-exportTemplate*** indicata nella tabella precedente definisce il percorso delle configurazioni di esportazione dell&#39;app. Impostate questa proprietà per creare e modificare le risorse condivise.

Le risorse seguenti descrivono l’esportazione di contenuti da Adobe Experience Manager (AEM) per il caricamento  AEM Mobile.

Gli articoli contengono contenuto che deve essere esportato e caricato. Alcuni di questi contenuti possono essere condivisi tra articoli diversi.

Utilizzate [ContentSync](/help/mobile/mobile-ondemand-contentsync.md) per raccogliere i contenuti e creare un pacchetto ***Risorse condivise***.

La configurazione ContentSync trovata in **&lt;dps-exportTemplate>/dps-article>** deve essere configurata per esportare tutto il contenuto un articolo richiesto per il rendering statico delle proprietà sul dispositivo.

>[!CAUTION]
>
>Per visualizzare le risorse condivise di esempio, potete eseguire le operazioni seguenti solo se avete:
>
>* installato il contenuto di esempio
>* esecuzione AEM&#39;istanza
>* nessun contesto personalizzato configurato o una porta diversa

>



Per visualizzare un esempio di risorsa condivisa, procedere come segue:

1. Aprite il CRXDE Lite sul server AEM.
1. Andate a questo percorso [/etc/contentsync/templates/dps-we-illimitato-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article) per visualizzare le risorse condivise di esempio.

   Potete visualizzare tutte le proprietà necessarie per creare le risorse condivise come illustrato nella figura seguente:

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>Gli articoli devono essere caricati o esportati in  AEM Mobile On-demand Services quando cambia il contenuto di un articolo.

