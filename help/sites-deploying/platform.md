---
title: Introduzione alla piattaforma AEM
seo-title: Introduction to the AEM Platform
description: Questo articolo fornisce una panoramica generale della piattaforma AEM e dei suoi componenti più importanti.
seo-description: This article provides a general overview of the AEM platform and its most important components.
uuid: 214d4c49-1f5c-432c-a2c0-c1fbdceee716
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: fccf9a0f-ebab-45ab-8460-84c86b3c4192
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/introduction-to-oak
exl-id: 8ee5f4ff-648d-45ea-a51e-894cd4385e62
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# Introduzione alla piattaforma AEM{#introduction-to-the-aem-platform}

La piattaforma AEM in AEM 6 si basa su Apache Jackrabbit Oak.

Apache Jackrabbit Oak è uno sforzo per implementare un archivio di contenuti gerarchici scalabile e performante da utilizzare come base dei siti web moderni e di altre applicazioni di contenuti esigenti.

Sostituisce Jackrabbit 2 e viene utilizzato da AEM 6 come backend predefinito per il relativo archivio di contenuti, CRX.

## Principi e obiettivi di progettazione {#design-principles-and-goals}

Oak implementa le [JSR-283](https://www.day.com/day/en/products/jcr/jsr-283.html) (JCR 2.0) specifiche. I suoi principali obiettivi sono:

* Supporto migliorato per archivi di grandi dimensioni
* Più nodi cluster distribuiti per un&#39;elevata disponibilità
* Prestazioni migliori
* Supporto per molti nodi figlio e livelli di controllo degli accessi

## Concetto di architettura {#architecture-concept}

![chlimage_1-84](assets/chlimage_1-84.png)

### Archiviazione {#storage}

Lo scopo del livello di storage è:

* Implementare un modello ad albero
* Rendere lo storage collegabile
* Fornire un meccanismo di clustering

### Oak Core {#oak-core}

Oak Core aggiunge diversi livelli al livello di archiviazione:

* Controlli a livello di accesso
* Ricerca e indicizzazione
* Osservazione

### Oak JCR {#oak-jcr}

L&#39;obiettivo principale di Oak JCR è quello di trasformare la semantica JCR in operazioni ad albero. È inoltre responsabile:

* Implementazione dell’API JCR
* Contenenti hook di commit che implementano vincoli JCR

Inoltre, le implementazioni non-Java sono ora possibili e fanno parte del concetto Oak JCR.

## Panoramica sullo storage {#storage-overview}

Il livello di archiviazione Oak fornisce un livello di astrazione per l&#39;effettivo archiviazione del contenuto.

Al momento sono disponibili due implementazioni di storage in AEM6: **Archiviazione Tar** e **Archiviazione MongoDB**.

### Archiviazione Tar {#tar-storage}

Lo storage Tar utilizza file tar. Memorizza il contenuto come vari tipi di record all’interno di segmenti più grandi. Le scritture contabili vengono utilizzate per tenere traccia dello stato più recente dell’archivio.

Ci sono diversi principi chiave di progettazione intorno a cui è stato costruito:

* **Segmenti immutabili**

Il contenuto viene memorizzato in segmenti di dimensioni fino a 256 KiB. Sono immutabili, il che rende facile memorizzare nella cache i segmenti a cui si accede di frequente e riduce gli errori di sistema che possono danneggiare l’archivio.

Ogni segmento è identificato da un identificatore univoco (UUID) e contiene un sottoinsieme continuo della struttura del contenuto. Inoltre, i segmenti possono fare riferimento ad altri contenuti. Ogni segmento mantiene un elenco di UUID di altri segmenti di riferimento.

* **Località**

I record correlati come un nodo e i relativi figli immediati vengono solitamente memorizzati nello stesso segmento. Questo rende la ricerca dell&#39;archivio molto veloce ed evita la maggior parte degli errori di cache per i clienti tipici che accedono a più di un nodo correlato per sessione.

* **Compattezza**

La formattazione dei record è ottimizzata per le dimensioni per ridurre i costi di I/O e per adattare il maggior numero possibile di contenuti nelle cache.

### Archiviazione Mongo {#mongo-storage}

Lo storage MongoDB sfrutta MongoDB per la condivisione e il clustering. La struttura dell&#39;archivio viene mantenuta in un database MongoDB in cui ogni nodo è un documento separato.

Ha diverse particolarità:

* Revisioni

Per ogni aggiornamento (commit) del contenuto, viene creata una nuova revisione. Una revisione è fondamentalmente una stringa costituita da tre elementi:

1. Una marca temporale derivata dall&#39;ora di sistema del computer in cui è stata generata
1. Un contatore per distinguere le revisioni create con la stessa marca temporale
1. ID nodo cluster in cui è stata creata la revisione

* Rami

I rami sono supportati, il che consente al client di mettere in scena più modifiche e di renderle visibili con una singola chiamata di unione.

* Documenti precedenti

L&#39;archiviazione MongoDB aggiunge dati a un documento con ogni modifica. Tuttavia, elimina i dati solo se viene attivata esplicitamente una pulizia. I dati precedenti vengono spostati quando viene soddisfatta una determinata soglia. I documenti precedenti contengono solo dati immutabili, il che significa che contengono solo revisioni salvate e unite.

* Metadati nodo cluster

I dati sui nodi del cluster attivi e inattivi vengono conservati nel database per facilitare le operazioni del cluster.

Configurazione cluster AEM tipica con archiviazione MongoDB:

![chlimage_1-85](assets/chlimage_1-85.png)

## Quali sono le differenze rispetto a Jackrabbit 2? {#what-is-different-from-jackrabbit}

Poiché Oak è progettato per essere compatibile con lo standard JCR 1.0, non ci saranno quasi modifiche a livello di utente. Tuttavia, ci sono alcune differenze notevoli che è necessario tenere in considerazione quando si imposta un&#39;installazione di AEM basata su Oak:

* Oak non crea indici automaticamente. Per questo motivo, se necessario, sarà necessario creare indici personalizzati.
* A differenza di Jackrabbit 2, dove le sessioni riflettono sempre lo stato più recente dell’archivio, con Oak una sessione riflette una vista stabile dell’archivio dal momento in cui la sessione è stata acquisita. Questo è dovuto al modello MVCC su cui si basa Oak.
* Gli elementi di pari livello con lo stesso nome (SNS) non sono supportati in Oak.

## Documentazione correlata ad altre piattaforme {#other-platform-related-documentation}

Per ulteriori informazioni sulla piattaforma AEM, consulta anche gli articoli seguenti:

* [Configurazione di Node Stores e Data Store in AEM 6](/help/sites-deploying/data-store-config.md)
* [Query e indicizzazione Oak](/help/sites-deploying/queries-and-indexing.md)
* [Elementi di storage in AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md)
* [AEM con MongoDB](/help/sites-deploying/aem-with-mongodb.md)
