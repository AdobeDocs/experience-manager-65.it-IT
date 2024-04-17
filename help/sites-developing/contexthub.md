---
title: ContextHub
description: ContextHub è un framework per l’archiviazione, la manipolazione e la presentazione dei dati contestuali
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 3fd50655-7461-4900-a3b8-c01b04c7ba7a
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# ContextHub{#contexthub}

ContextHub è un framework per l’archiviazione, la manipolazione e la presentazione dei dati contestuali. L’API JavaScript lato client ti consente di accedere ai dati per personalizzare il contenuto.

>[!NOTE]
>
>Il [Implementazione di riferimento We.Retail](/help/sites-developing/we-retail.md) implementa ContextHub e può fungere da riferimento durante l’integrazione di ContextHub nel tuo progetto.

>[!CAUTION]
>
>Percorso contenente la configurazione ContextHub di esempio utilizzata dall&#39;oggetto [Implementazione di riferimento We.Retail](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`) deve essere utilizzato solo come riferimento per la creazione di una configurazione personalizzata.
>
>Non utilizzare in un progetto come configurazione ContextHub personalizzata.

## Persistenza {#persistence}

ContextHub archivia i dati contestuali persistenti sul client. L’API JavaScript di ContextHub consente di accedere agli store per creare, aggiornare ed eliminare i dati in base alle esigenze. ContextHub rappresenta un livello dati sulle pagine.

Ogni archivio ContextHub è un’istanza di un tipo di archivio predefinito:

* ContextHub fornisce diversi [tipi di archivio di esempio](/help/sites-developing/ch-samplestores.md).
* Utilizzare le console AEM per [crea store](ch-configuring.md#creating-a-contexthub-store).
* Gli sviluppatori possono [creare tipi di store personalizzati](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).
* Gli sviluppatori possono [accedere ai dati dell’archivio](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) tramite JavaScript.

## Segmentazione {#segmentation}

ContextHub include un motore di segmentazione che gestisce i segmenti e determina quali segmenti vengono risolti per il contesto corrente. Sono definiti diversi segmenti. È possibile utilizzare l’API JavaScript per: [determinare i segmenti risolti](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## Presentazione {#presentation}

Il [Barra degli strumenti di ContextHub](/help/sites-authoring/ch-previewing.md) consente agli addetti al marketing e agli autori di visualizzare e manipolare i dati dell’archivio per simulare l’esperienza utente durante l’authoring delle pagine. La barra degli strumenti è costituita da gruppi di moduli di interfaccia utente che forniscono accesso agli store ContextHub.

Ogni modulo dell’interfaccia utente ContextHub è un’istanza di un tipo di modulo predefinito:

* ContextHub fornisce diversi [tipi di moduli di esempio](/help/sites-developing/ch-samplemodules.md).
* Utilizzare le console AEM per [aggiungere moduli di interfaccia utente](ch-configuring.md#adding-a-ui-module), e a [raggrupparli in modalità interfaccia utente](ch-configuring.md#adding-a-ui-mode).

* Gli sviluppatori possono [creare tipi di moduli personalizzati](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

Gli sviluppatori devono: [aggiungere il componente ContextHub alla pagina](/help/sites-developing/ch-adding.md).
