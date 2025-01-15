---
title: Creazione configurazione esportazione risorse condivise
description: Segui questa pagina per scoprire come esportare risorse condivise da Adobe Experience Manager (AEM) per caricarle in AEM Mobile.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Creazione configurazione esportazione risorse condivise{#creating-shared-resources-export-configuration}

{{ue-over-mobile}}

>[!CAUTION]
>
>**Prerequisito**:
>
>Prima di scoprire come creare e modificare le risorse condivise, consulta [Sincronizzazione contenuti](/help/mobile/mobile-ondemand-contentsync.md) per comprendere i concetti di base.

Gli utenti di dispositivi mobili Adobe Experience Manager (AEM) utilizzano la sincronizzazione dei contenuti per esportare contenuti live in contenuti statici da utilizzare nelle app mobili. Questa esportazione si verifica quando i contenuti vengono caricati in Mobile On-Demand Services da AEM Mobile.

La proprietà ***dps-exportTemplate*** indicata nella tabella precedente definisce il percorso delle configurazioni di esportazione dell&#39;app. Impostare questa proprietà per creare e modificare le risorse condivise.

Le risorse seguenti descrivono l’esportazione di risorse condivise da AEM per il caricamento in AEM Mobile.

Le risorse HTML condivise consentono agli articoli di condividere risorse HTML che altrimenti verrebbero duplicate per tutti gli articoli e che possono includere icone, font, JavaScript e CSS.

La configurazione di sincronizzazione contenuti trovata in **&lt;dps-exportTemplate>/dps-HTMLResources>** deve essere configurata in modo da esportare tutto il contenuto richiesto da un articolo per il rendering statico delle proprietà sul dispositivo.

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
1. Individua il percorso *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)* per visualizzare le risorse condivise di esempio.

   Puoi visualizzare tutte le proprietà necessarie per creare le risorse condivise, come illustrato nella figura seguente:

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>Le risorse condivise devono essere caricate o esportate in AEM Mobile On-demand Services quando una qualsiasi delle risorse condivise cambia.
