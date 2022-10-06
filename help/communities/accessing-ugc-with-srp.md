---
title: Accesso a UGC con SRP
seo-title: Accessing UGC with SRP
description: Quando un sito è configurato per utilizzare ASRP o MSRP, l'UGC effettivo non viene memorizzato nell'archivio nodi AEM (JCR)
seo-description: When a site is configured to use ASRP or MSRP, the actual UGC is not be stored in AEM's node store (JCR)
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
exl-id: 1157366f-2cc5-46e4-8ec6-e66fe5d0a0f6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Accesso a UGC con SRP {#accessing-ugc-with-srp}

## Informazioni sull’SRP {#about-srp}

Tutti i componenti e le funzioni di AEM Communities sono incorporati nella [quadro della componente sociale (SCF)](/help/communities/scf.md), che chiama l&#39;API SocialResourceProvider per accedere a tutti i contenuti generati dall&#39;utente (UGC).

Prima della creazione di un sito community, la funzione [provider di risorse di archiviazione (SRP)](/help/communities/working-with-srp.md) deve essere configurato per selezionare un&#39;implementazione coerente con il sottostante [topologia](/help/communities/topologies.md). Le implementazioni SRP si basano su tre opzioni di storage:

1. [ASRP](/help/communities/asrp.md) - Adobe on-demand storage
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## Informazioni sullo storage UGC {#about-ugc-storage}

Ciò che è importante sapere sull&#39;archiviazione di UGC è che, quando un sito è configurato per utilizzare ASRP o MSRP, l&#39;UGC effettivo non è memorizzato in AEM [archivio nodi](/help/sites-deploying/data-store-config.md) (JCR).

Anche se ci possono essere nodi in JCR che ombreggiano l&#39;UGC per fornire metadati utili, questi nodi non devono essere confusi con l&#39;UGC effettivo.

Vedi [Panoramica del provider di risorse di archiviazione.](/help/communities/srp.md)

## Best practice {#best-practice}

Quando si sviluppano componenti personalizzati, gli sviluppatori devono fare attenzione al codice indipendentemente dalla topologia attualmente selezionata, mantenendo così la flessibilità per passare a una nuova topologia in futuro.

### Supponiamo che JCR non sia disponibile {#assume-jcr-not-available}

È opportuno evitare i metodi specifici di JCR.

Metodi di utilizzo :

* API Sling (risorsa Sling)

   * non presumere che ci siano nodi JCR

* Eventi OSGi

   * non presumere che ci siano eventi JCR

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

Metodi per evitare :

* API nodo
* Eventi JCR
* avviatori del flusso di lavoro (che utilizzano eventi JCR)

### Utilizzare le raccolte di ricerca {#use-search-collections}

I diversi SRP possono avere linguaggi di query nativi diversi. Si consiglia di utilizzare i metodi [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) per eseguire il linguaggio di query appropriato.

Per ulteriori informazioni, consulta [Nozioni di base sulla ricerca](/help/communities/search-implementation.md).

## Riferimenti {#resources}

* [Archiviazione dei contenuti della community](/help/communities/working-with-srp.md) - discute le scelte SRP disponibili per un negozio comune UGC
* [Panoramica del provider di risorse di storage](/help/communities/srp.md) - introduzione e utilizzo dell&#39;archivio
* [Essenze SRP e UGC](/help/communities/srp-and-ugc.md) - Metodi e esempi di utilità SRP
* [Nozioni di base sulla ricerca](/help/communities/search-implementation.md) - informazioni essenziali per la ricerca UGC
* [Refactoring di SocialUtils](/help/communities/socialutils.md) - mappatura di metodi di utilità obsoleti ai metodi di utilità SRP correnti
