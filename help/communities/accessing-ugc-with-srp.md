---
title: Accesso a UGC con SRP
seo-title: Accesso a UGC con SRP
description: Quando un sito è configurato per utilizzare ASRP o MSRP, l'UGC effettivo non viene memorizzato nell'archivio nodi di AEM (JCR)
seo-description: Quando un sito è configurato per utilizzare ASRP o MSRP, l'UGC effettivo non viene memorizzato nell'archivio nodi di AEM (JCR)
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
translation-type: tm+mt
source-git-commit: 70e6f2d8366456e5091b7b775dc40914948921ab

---


# Accesso a UGC con SRP{#accessing-ugc-with-srp}

## Informazioni su SRP {#about-srp}

Tutti i componenti e le funzionalità di AEM Communities sono basati sul framework di componenti [social network (SCF)](/help/communities/scf.md), che chiama l&#39;API SocialResourceProvider per accedere a tutti i contenuti generati dall&#39;utente (UGC).

Prima di creare un sito community, è necessario configurare il provider di risorse di [storage (SRP)](/help/communities/working-with-srp.md) per selezionare un&#39;implementazione coerente con la [topologia](/help/communities/topologies.md)sottostante. Le implementazioni SRP si basano su tre opzioni di storage:

1. [ASRP](/help/communities/asrp.md) - Archiviazione su richiesta Adobe
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## Archiviazione UGC {#about-ugc-storage}

Ciò che è importante sapere sull&#39;archiviazione di UGC è che, quando un sito è configurato per utilizzare ASRP o MSRP, l&#39;UGC effettivo non viene memorizzato nello store [](/help/sites-deploying/data-store-config.md) nodi di AEM (JCR).

Anche se in JCR possono essere presenti nodi che oscurano l&#39;UGC per fornire metadati utili, questi nodi non devono essere confusi con l&#39;UGC effettivo.

Vedere Panoramica sui provider delle risorse [di storage.](/help/communities/srp.md)

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

### Usa raccolte di ricerca {#use-search-collections}

Diversi SRP possono avere lingue di query native diverse. È consigliabile utilizzare i metodi del pacchetto [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) per eseguire la lingua di query appropriata.

Per ulteriori informazioni, consulta [Ricerca in Essentials](/help/communities/search-implementation.md).

## Risorse {#resources}

* [Archiviazione](/help/communities/working-with-srp.md) dei contenuti della community - illustra le opzioni SRP disponibili per uno store comune UGC
* [Panoramica](/help/communities/srp.md) del provider di risorse di storage - introduzione e utilizzo del repository
* [Caratteristiche essenziali di SRP e UGC](/help/communities/srp-and-ugc.md) - Metodi e esempi di utilità SRP
* [Ricerca Essentials](/help/communities/search-implementation.md) - informazioni essenziali per la ricerca UGC
* [Refactoring](/help/communities/socialutils.md) SocialUtils - mappatura di metodi di utilità obsoleti ai metodi di utilità SRP correnti

