---
title: Creazione della configurazione di esportazione degli articoli
seo-title: Creating Article Export Configuration
description: Segui questa pagina per informazioni sull’esportazione di contenuti da Adobe Experience Manager (AEM) per il caricamento in AEM Mobile.
seo-description: Follow this page to learn about exporting content from Adobe Experience Manager (AEM) for upload to AEM Mobile.
uuid: 089bc15b-669e-4623-bdbb-fd9abf46e098
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: bc681589-5d46-44cd-888d-b0722a2fd006
exl-id: 5295f383-3b46-4456-9177-65de68e39a85
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# Creazione della configurazione di esportazione degli articoli{#creating-article-export-configuration}

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

Le risorse seguenti descrivono l’esportazione di contenuti da Adobe Experience Manager (AEM) per il caricamento in AEM Mobile.

Gli articoli hanno contenuti che devono essere esportati e caricati. Alcuni di questi contenuti possono essere condivisi tra gli articoli.

Utilizzo [ContentSync](/help/mobile/mobile-ondemand-contentsync.md) per raccogliere i contenuti e creare un ***Risorse condivise*** pacchetto.

Configurazione ContentSync trovata in **&lt;dps-exporttemplate>/dps-article>** deve essere configurato per esportare tutto il contenuto di un articolo richiesto per il rendering statico delle proprietà sul dispositivo.

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
1. Sfoglia questo percorso [/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article), per visualizzare le risorse condivise di esempio.

   Puoi visualizzare tutte le proprietà necessarie per la creazione delle risorse condivise, come illustrato nella figura seguente:

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>Gli articoli devono essere caricati o esportati in AEM Mobile On-demand Services quando cambia il contenuto di un articolo.
