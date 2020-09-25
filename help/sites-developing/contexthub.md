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
>L’implementazione [di riferimento](/help/sites-developing/we-retail.md) We.Retail implementa ContextHub e può fungere da riferimento quando integri ContextHub nel tuo progetto.

>[!CAUTION]
>
>Il percorso contenente la configurazione ContextHub di esempio utilizzata dall&#39;implementazione [di riferimento](/help/sites-developing/we-retail.md) We.Retail ( `/libs/settings/cloudsettings/legacy`) deve essere utilizzato solo come riferimento per la creazione di una propria configurazione.
>
>Non deve essere utilizzato in un progetto come configurazione ContextHub personalizzata.

## Persistenza {#persistence}

ContextHub memorizza i dati contestuali persistenti sul client. L&#39;API ContextHub Javascript consente di accedere agli store per creare, aggiornare ed eliminare i dati secondo necessità. ContextHub rappresenta pertanto un livello dati sulle pagine.

Ciascun archivio ContextHub è un&#39;istanza di un tipo di store predefinito:

* ContextHub fornisce diversi tipi [di archivio di](/help/sites-developing/ch-samplestores.md)esempio.
* Utilizzate AEM console per [creare store](ch-configuring.md#creating-a-contexthub-store).
* Gli sviluppatori possono [creare tipi](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)di store personalizzati.
* Gli sviluppatori possono [accedere ai dati](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) dell&#39;archivio tramite Javascript.

## Segmentazione {#segmentation}

ContextHub include un motore di segmentazione che gestisce i segmenti e determina quali segmenti vengono risolti per il contesto corrente. Sono definiti diversi segmenti. Puoi utilizzare l&#39;API Javascript per [determinare i segmenti](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments)risolti.

## Presentazione {#presentation}

La barra degli strumenti [](/help/sites-authoring/ch-previewing.md) ContextHub consente agli esperti di marketing e agli autori di visualizzare e manipolare i dati dell&#39;archivio per simulare l&#39;esperienza utente durante l&#39;authoring delle pagine. La barra degli strumenti è composta da gruppi di moduli dell’interfaccia utente che forniscono l’accesso agli store ContextHub.

Ciascun modulo dell’interfaccia utente ContextHub è un’istanza di tipo di modulo predefinito:

* ContextHub offre diversi tipi [di moduli di](/help/sites-developing/ch-samplemodules.md)esempio.
* Utilizzate AEM console per [aggiungere moduli](ch-configuring.md#adding-a-ui-module)dell&#39;interfaccia utente e per [raggrupparli in modalità](ch-configuring.md#adding-a-ui-mode)di interfaccia.

* Gli sviluppatori possono [creare tipi](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)di moduli personalizzati.

Gli sviluppatori devono [aggiungere il componente ContextHub alla pagina](/help/sites-developing/ch-adding.md).
