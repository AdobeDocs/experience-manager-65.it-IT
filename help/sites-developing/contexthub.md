---
title: ContextHub
seo-title: ContextHub
description: ContextHub è un framework per la memorizzazione, la manipolazione e la presentazione dei dati contestuali
seo-description: ContextHub è un framework per la memorizzazione, la manipolazione e la presentazione dei dati contestuali
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---


# ContextHub{#contexthub}

ContextHub è un framework per la memorizzazione, la manipolazione e la presentazione dei dati contestuali. L&#39;API Javascript lato client consente di accedere ai dati per la personalizzazione del contenuto.

>[!NOTE]
>
>L&#39;implementazione di riferimento di [We.Retail](/help/sites-developing/we-retail.md) implementa ContextHub e può fungere da riferimento quando integri ContextHub nel tuo progetto.

>[!CAUTION]
>
>Il percorso contenente la configurazione ContextHub di esempio utilizzata dall&#39;implementazione di riferimento [We.Retail](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`) deve essere utilizzato solo come riferimento per la creazione di una configurazione personalizzata.
>
>Non deve essere utilizzato in un progetto come configurazione ContextHub personalizzata.

## Persistenza {#persistence}

ContextHub memorizza i dati contestuali persistenti sul client. L&#39;API ContextHub Javascript consente di accedere agli store per creare, aggiornare ed eliminare i dati secondo necessità. ContextHub rappresenta pertanto un livello dati sulle pagine.

Ciascun archivio ContextHub è un&#39;istanza di un tipo di store predefinito:

* ContextHub fornisce diversi [tipi di store di esempio](/help/sites-developing/ch-samplestores.md).
* Utilizzate AEM console per [creare store](ch-configuring.md#creating-a-contexthub-store).
* Gli sviluppatori possono [creare tipi di store personalizzati](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).
* Gli sviluppatori possono [accedere ai dati dell&#39;archivio](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) tramite Javascript.

## Segmentazione {#segmentation}

ContextHub include un motore di segmentazione che gestisce i segmenti e determina quali segmenti vengono risolti per il contesto corrente. Sono definiti diversi segmenti. Puoi utilizzare l&#39;API Javascript per [determinare i segmenti risolti](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## Presentazione {#presentation}

La [barra degli strumenti ContextHub](/help/sites-authoring/ch-previewing.md) consente agli esperti di marketing e agli autori di visualizzare e manipolare i dati dello store per simulare l&#39;esperienza utente durante l&#39;authoring delle pagine. La barra degli strumenti è composta da gruppi di moduli dell’interfaccia utente che forniscono l’accesso agli store ContextHub.

Ciascun modulo dell’interfaccia utente ContextHub è un’istanza di tipo di modulo predefinito:

* ContextHub fornisce diversi [tipi di moduli di esempio](/help/sites-developing/ch-samplemodules.md).
* Utilizzare AEM console per [aggiungere moduli dell&#39;interfaccia utente](ch-configuring.md#adding-a-ui-module) e per [raggrupparli in modalità di interfaccia utente](ch-configuring.md#adding-a-ui-mode).

* Gli sviluppatori possono [creare tipi di moduli personalizzati](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

Gli sviluppatori devono [aggiungere il componente ContextHub alla pagina](/help/sites-developing/ch-adding.md).
