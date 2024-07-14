---
title: Accesso a UGC con SRP
description: Quando un sito è configurato per l’utilizzo di ASRP o MSRP, l’UGC effettivo non viene memorizzato nell’archivio dei nodi (JCR) dell’AEM
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

Tutti i componenti e le funzionalità di AEM Communities sono basati sul [framework di componenti social network (SCF)](/help/communities/scf.md), che chiama l&#39;API SocialResourceProvider per accedere a tutti i contenuti generati dagli utenti (UGC, User Generated Content).

Prima di creare un sito community, è necessario configurare il provider di risorse di archiviazione [SRP](/help/communities/working-with-srp.md) per selezionare un&#39;implementazione coerente con la [topologia](/help/communities/topologies.md) sottostante. Le implementazioni SRP si basano su tre opzioni di storage:

1. [ASRP](/help/communities/asrp.md) - Adobe archiviazione su richiesta
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## Informazioni sull’archiviazione UGC {#about-ugc-storage}

Ciò che è importante sapere sull&#39;archiviazione di UGC è che, quando un sito è configurato per l&#39;utilizzo di ASRP o MSRP, l&#39;UGC effettivo non viene archiviato nell&#39;[archivio nodi](/help/sites-deploying/data-store-config.md) (JCR) dell&#39;AEM.

Anche se in JCR possono esserci nodi che ombreggiano l’UGC per fornire metadati utili, questi non devono essere confusi con l’UGC effettivo.

Vedere [Panoramica provider risorse di archiviazione.](/help/communities/srp.md)

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

Diversi SRP possono avere lingue di query native diverse. Utilizzare i metodi del pacchetto [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) per eseguire il linguaggio di query appropriato.

Per ulteriori informazioni, vedere [Search Essentials](/help/communities/search-implementation.md).

## Riferimenti {#resources}

* [Archiviazione contenuto community](/help/communities/working-with-srp.md): illustra le scelte SRP disponibili per un archivio comune UGC
* [Panoramica del provider di risorse di archiviazione](/help/communities/srp.md) - introduzione e panoramica sull&#39;utilizzo dell&#39;archivio
* [Nozioni di base su SRP e UGC](/help/communities/srp-and-ugc.md) - Metodi ed esempi dell&#39;utilità SRP
* [Search Essentials](/help/communities/search-implementation.md) - informazioni essenziali per la ricerca UGC
* [Refactoring di SocialUtils](/help/communities/socialutils.md) - mapping dei metodi di utilità obsoleti ai metodi di utilità SRP correnti
