---
title: Creazione della configurazione di esportazione dell'articolo
description: Segui questa pagina per scoprire come esportare i contenuti da Adobe Experience Manager (AEM) per caricarli in AEM Mobile.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 5295f383-3b46-4456-9177-65de68e39a85
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 1%

---

# Creazione della configurazione di esportazione dell&#39;articolo{#creating-article-export-configuration}

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

Le risorse seguenti descrivono l’esportazione di contenuto da Adobe Experience Manager (AEM) per il caricamento in AEM Mobile.

Gli articoli hanno contenuti da esportare e caricare. Parte di questo contenuto può essere condiviso tra gli articoli.

Utilizzare [Sincronizzazione contenuti](/help/mobile/mobile-ondemand-contentsync.md) per raccogliere i contenuti e creare un ***Risorse condivise*** pacchetto.

Configurazione di ContentSync trovata in **&lt;dps-exporttemplate>/dps-article>** deve essere configurato per esportare tutto il contenuto di un articolo necessario per il rendering statico della proprietà sul dispositivo.

>[!CAUTION]
>
>Puoi eseguire i passaggi seguenti per visualizzare risorse condivise di esempio, solo se:
>
>* ha installato il contenuto di esempio
>* esecuzione dell’istanza AEM
>* nessun contesto personalizzato configurato o una porta diversa
>

Per visualizzare un esempio di risorsa condivisa, consulta i passaggi seguenti:

1. Apri CRXDE Liti sul server AEM.
1. Passa a questo percorso [/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article), per visualizzare le risorse condivise di esempio.

   Puoi visualizzare tutte le proprietà necessarie per creare le risorse condivise, come illustrato nella figura seguente:

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>Quando il contenuto di un articolo cambia, gli articoli devono essere caricati o esportati in AEM Mobile On-demand Services.
