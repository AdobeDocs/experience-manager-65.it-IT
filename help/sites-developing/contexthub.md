---
title: ContextHub
seo-title: ContextHub
description: ContextHub è un framework per la memorizzazione, la manipolazione e la presentazione dei dati contestuali
seo-description: ContextHub is a framework for storing, manipulating, and presenting context data
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
exl-id: 3fd50655-7461-4900-a3b8-c01b04c7ba7a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 1%

---

# ContextHub{#contexthub}

ContextHub è un framework per la memorizzazione, la manipolazione e la presentazione dei dati contestuali. L’API JavaScript lato client consente di accedere ai dati per la personalizzazione del contenuto.

>[!NOTE]
>
>La [Implementazione di riferimento di We.Retail](/help/sites-developing/we-retail.md) implementa ContextHub e può fungere da riferimento mentre integri ContextHub nel tuo progetto.

>[!CAUTION]
>
>Il percorso contenente la configurazione ContextHub di esempio utilizzata da [Implementazione di riferimento di We.Retail](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`) deve essere utilizzato solo come riferimento per la creazione di una configurazione personalizzata.
>
>Non deve essere utilizzato in un progetto come configurazione ContextHub personalizzata.

## Persistenza {#persistence}

ContextHub memorizza i dati contestuali persistenti sul client. L’API Javascript di ContextHub consente di accedere agli archivi per creare, aggiornare ed eliminare i dati in base alle necessità. ContextHub rappresenta un livello di dati sulle pagine.

Ogni archivio ContextHub è un&#39;istanza di un tipo di archivio predefinito:

* ContextHub fornisce diversi [tipi di archivio di esempio](/help/sites-developing/ch-samplestores.md).
* Utilizzare le console AEM per [creare negozi](ch-configuring.md#creating-a-contexthub-store).
* Gli sviluppatori possono [creare tipi di archivio personalizzati](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).
* Gli sviluppatori possono [accesso ai dati dell&#39;archivio](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) via Javascript.

## Segmentazione {#segmentation}

ContextHub include un motore di segmentazione che gestisce i segmenti e determina quali segmenti vengono risolti per il contesto corrente. Sono definiti diversi segmenti. Puoi utilizzare l’API JavaScript per [determinare i segmenti risolti](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## Presentazione {#presentation}

La [Barra degli strumenti di ContextHub](/help/sites-authoring/ch-previewing.md) consente agli esperti di marketing e agli autori di visualizzare e manipolare i dati dell’archivio per simulare l’esperienza utente durante l’authoring delle pagine. La barra degli strumenti è costituita da gruppi di moduli di interfaccia utente che forniscono accesso agli archivi ContextHub.

Ciascun modulo dell’interfaccia utente di ContextHub è un’istanza di un tipo di modulo predefinito:

* ContextHub fornisce diversi [tipi di moduli di esempio](/help/sites-developing/ch-samplemodules.md).
* Utilizzare le console AEM per [aggiungere moduli di interfaccia utente](ch-configuring.md#adding-a-ui-module)e a [raggrupparli in modalità interfaccia utente](ch-configuring.md#adding-a-ui-mode).

* Gli sviluppatori possono [creare tipi di moduli personalizzati](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

Gli sviluppatori devono [aggiungi il componente ContextHub alla pagina](/help/sites-developing/ch-adding.md).
