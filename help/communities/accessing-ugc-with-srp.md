---
title: Accesso a UGC con SRP
seo-title: Accesso a UGC con SRP
description: Quando un sito è configurato per l'utilizzo di ASRP o MSRP, l'UGC effettivo non viene memorizzato in AEM archivio nodi (JCR)
seo-description: Quando un sito è configurato per l'utilizzo di ASRP o MSRP, l'UGC effettivo non viene memorizzato in AEM archivio nodi (JCR)
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
translation-type: tm+mt
source-git-commit: 974d58efa560b90234d5121a11bdb445c7bf94cf
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---


# Accesso a UGC con SRP {#accessing-ugc-with-srp}

## Informazioni su SRP {#about-srp}

Tutti  componenti e funzionalità AEM Communities sono basati sul [social component framework (SCF)](/help/communities/scf.md), che chiama l&#39;API SocialResourceProvider per accedere a tutti i contenuti generati dall&#39;utente (UGC).

Prima di creare un sito community, è necessario configurare il [provider di risorse di storage (SRP)](/help/communities/working-with-srp.md) per selezionare un&#39;implementazione coerente con la [topologia sottostante](/help/communities/topologies.md). Le implementazioni SRP si basano su tre opzioni di storage:

1. [ASRP](/help/communities/asrp.md) -  Adobe su richiesta
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md)  - JCR

## Archiviazione UGC {#about-ugc-storage}

Ciò che è importante sapere sull&#39;archiviazione di UGC è che, quando un sito è configurato per utilizzare ASRP o MSRP, l&#39;UGC effettivo non è memorizzato in AEM [node store](/help/sites-deploying/data-store-config.md) (JCR).

Anche se in JCR possono essere presenti nodi che oscurano l&#39;UGC per fornire metadati utili, questi nodi non devono essere confusi con l&#39;UGC effettivo.

Vedere [Panoramica sui provider di risorse di storage.](/help/communities/srp.md)

## Best practice {#best-practice}

Quando si sviluppano componenti personalizzati, gli sviluppatori devono prestare attenzione alla codifica indipendentemente dalla topologia scelta, conservando la flessibilità necessaria per passare a una nuova topologia in futuro.

### Presupponi JCR non disponibile {#assume-jcr-not-available}

I metodi specifici per JCR dovrebbero essere evitati.

Metodi di utilizzo:

* API Sling (risorsa Sling)

   * non si presuppone che siano presenti nodi JCR

* Eventi OSGi

   * non presupporre che siano presenti eventi JCR

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

Metodi per evitare :

* API nodo
* Eventi JCR
* avviatori di workflow (che utilizzano eventi JCR)

### Utilizzare raccolte di ricerca {#use-search-collections}

Diversi SRP possono avere lingue di query native diverse. È consigliabile utilizzare i metodi del pacchetto [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) per eseguire il linguaggio di query appropriato.

Per ulteriori informazioni, vedere [Ricerca di Essentials](/help/communities/search-implementation.md).

## Riferimenti {#resources}

* [Archiviazione](/help/communities/working-with-srp.md)  dei contenuti della community: vengono illustrate le opzioni SRP disponibili per uno store comune UGC
* [Panoramica](/help/communities/srp.md)  del provider di risorse di storage - introduzione e utilizzo del repository
* [Funzioni essenziali](/help/communities/srp-and-ugc.md)  SRP e UGC - Metodi di utilità SRP ed esempi
* [Ricerca Essentials](/help/communities/search-implementation.md)  - informazioni essenziali per la ricerca UGC
* [Refactoring](/help/communities/socialutils.md)  SocialUtils: mappatura di metodi di utilità obsoleti ai metodi di utilità SRP correnti

