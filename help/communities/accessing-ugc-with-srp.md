---
title: Accesso a UGC con SRP
description: Quando un sito è configurato per l’utilizzo di ASRP o MSRP, l’UGC effettivo non viene memorizzato nell’archivio dei nodi AEM (JCR)
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 1157366f-2cc5-46e4-8ec6-e66fe5d0a0f6
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Accesso a UGC con SRP {#accessing-ugc-with-srp}

## Informazioni su SRP {#about-srp}

Tutti i componenti e le funzioni di AEM Communities sono basati su [framework della componente social network (SCF)](/help/communities/scf.md), che chiama l&#39;API SocialResourceProvider per accedere a tutti i contenuti generati dagli utenti (UGC, User Generated Content).

Prima della creazione di un sito community, [provider di risorse di archiviazione (SRP)](/help/communities/working-with-srp.md) deve essere configurato per selezionare un’implementazione coerente con [topologia](/help/communities/topologies.md). Le implementazioni SRP si basano su tre opzioni di storage:

1. [ASRP](/help/communities/asrp.md) - storage on-demand Adobe
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## Informazioni sull’archiviazione UGC {#about-ugc-storage}

Ciò che è importante sapere sullo storage di UGC è che, quando un sito è configurato per l&#39;uso di ASRP o MSRP, l&#39;UGC effettivo non viene memorizzato nell&#39;AEM [archivio nodi](/help/sites-deploying/data-store-config.md) (JCR)

Anche se in JCR possono esserci nodi che ombreggiano l’UGC per fornire metadati utili, questi non devono essere confusi con l’UGC effettivo.

Consulta [Panoramica del provider di risorse di archiviazione.](/help/communities/srp.md)

## Best practice {#best-practice}

Durante lo sviluppo di componenti personalizzati, gli sviluppatori devono prestare attenzione a codificare indipendentemente dalla topologia selezionata, mantenendo così la flessibilità necessaria per passare in futuro a una nuova topologia.

### Supponiamo che JCR non sia disponibile {#assume-jcr-not-available}

Devono essere evitati metodi specifici per JCR.

Metodi da utilizzare:

* API Sling (risorsa Sling)

   * non presumere che ci siano nodi JCR

* Eventi OSGi

   * non presumere che ci siano eventi JCR

* [UtilitàRisorseSocial](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

Metodi da evitare:

* API nodo
* Eventi JCR
* moduli di avvio dei flussi di lavoro (che utilizzano eventi JCR)

### Utilizzare le raccolte di ricerca {#use-search-collections}

Diversi SRP possono avere lingue di query native diverse. Utilizzare i metodi di [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) per eseguire il linguaggio di query appropriato.

Per ulteriori informazioni, consulta [Search Essentials](/help/communities/search-implementation.md).

## Riferimenti {#resources}

* [Archiviazione contenuti community](/help/communities/working-with-srp.md) - discute le scelte SRP disponibili per un common store UGC
* [Panoramica del provider di risorse di archiviazione](/help/communities/srp.md) - introduzione e panoramica sull’utilizzo dell’archivio
* [Nozioni di base su SRP e UGC](/help/communities/srp-and-ugc.md) - Metodi ed esempi di utilità SRP
* [Search Essentials](/help/communities/search-implementation.md) - informazioni essenziali per la ricerca UGC
* [Refactoring SocialUtils](/help/communities/socialutils.md) - mappatura dei metodi di utilità obsoleti sui metodi di utilità SRP correnti
