---
title: Introduzione alla piattaforma AEM
seo-title: Introduzione alla piattaforma AEM
description: Questo articolo fornisce una panoramica generale della piattaforma AEM e dei suoi componenti più importanti.
seo-description: Questo articolo fornisce una panoramica generale della piattaforma AEM e dei suoi componenti più importanti.
uuid: 214d4c49-1f5c-432c-a2c0-c1fbdceee716
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: fccf9a0f-ebab-45ab-8460-84c86b3c4192
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/introduction-to-oak
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 0%

---


# Introduzione alla piattaforma AEM{#introduction-to-the-aem-platform}

La piattaforma AEM in AEM 6 si basa su Apache Jackrabbit Oak.

Apache Jackrabbit Oak è uno sforzo per implementare un archivio di contenuti gerarchici scalabile e performante da usare come base per i siti Web moderni e altre applicazioni di contenuto esigenti.

È il successore di Jackrabbit 2 ed è utilizzato da AEM 6 come backend predefinito per il suo repository di contenuti, CRX.

## Principi e obiettivi di progettazione {#design-principles-and-goals}

Oak implementa la specifica [JSR-283](https://www.day.com/day/en/products/jcr/jsr-283.html) (JCR 2.0). I suoi obiettivi principali sono:

* Migliore supporto per i grandi repository
* Più nodi cluster distribuiti per un&#39;elevata disponibilità
* Prestazioni migliori
* Supporto per molti nodi figlio e livelli di controllo degli accessi

## Concetto di architettura {#architecture-concept}

![chlimage_1-84](assets/chlimage_1-84.png)

### Archiviazione {#storage}

Lo scopo del livello Storage è di:

* Implementare un modello ad albero
* Rendere lo storage collegabile
* Fornire un meccanismo di clustering

### Oak Core {#oak-core}

Oak Core aggiunge diversi livelli al livello di storage:

* Controlli del livello di accesso
* Ricerca e indicizzazione
* Osservazione

### Oak JCR {#oak-jcr}

L&#39;obiettivo principale di Oak JCR è trasformare la semantica JCR in operazioni ad albero. È inoltre responsabile di:

* Implementazione dell&#39;API JCR
* Contenenti ganci di commit che implementano i vincoli JCR

Inoltre, ora sono possibili implementazioni non Java e fanno parte del concetto Oak JCR.

## Panoramica sull&#39;archiviazione {#storage-overview}

Il livello di memorizzazione Oak fornisce un livello di astrazione per lo storage effettivo del contenuto.

Al momento sono disponibili due implementazioni di storage in AEM6: **Tar Storage** e **MongoDB Storage**.

### Archiviazione delle barre {#tar-storage}

L&#39;archiviazione Tar utilizza i file tar. Il contenuto viene memorizzato come vari tipi di record all&#39;interno di segmenti più grandi. Le scritture contabili vengono utilizzate per tenere traccia dello stato più recente della directory archivio.

Esistono diversi principi chiave di progettazione su cui è stato costruito:

* **Segmenti immutabili**

Il contenuto è memorizzato in segmenti con dimensioni fino a 256 KiB. Sono immutabili, che semplificano la memorizzazione nella cache dei segmenti a cui si accede di frequente e riducono gli errori di sistema che possono danneggiare il repository.

Ogni segmento è identificato da un identificatore univoco (UUID) e contiene un sottoinsieme continuo della struttura del contenuto. Inoltre, i segmenti possono fare riferimento ad altri contenuti. Ogni segmento tiene un elenco di UUID di altri segmenti di riferimento.

* **Località**

I record correlati come un nodo e i relativi elementi figlio immediati vengono generalmente memorizzati nello stesso segmento. Questo rende la ricerca nel repository molto veloce ed evita la maggior parte degli errori di cache per client tipici che accedono a più nodi correlati per sessione.

* **Compattezza**

La formattazione dei record è ottimizzata per ridurre i costi di I/O e per adattare il maggior numero possibile di contenuti nelle cache.

### Archiviazione Mongo {#mongo-storage}

Lo storage MongoDB utilizza MongoDB per la condivisione e il clustering. La struttura dell&#39;archivio è memorizzata in un database MongoDB in cui ogni nodo è un documento separato.

Essa presenta diverse particolarità:

* Revisioni

Per ogni aggiornamento (commit) del contenuto, viene creata una nuova revisione. Una revisione è sostanzialmente una stringa costituita da tre elementi:

1. Una marca temporale derivata dall&#39;ora di sistema del computer in cui è stata generata
1. Contatore per distinguere le revisioni create con la stessa marca temporale
1. ID nodo cluster in cui è stata creata la revisione

* Rami

Le diramazioni sono supportate, che consente al client di mettere in scena più modifiche e renderle visibili con una singola chiamata di unione.

* Documenti precedenti

L&#39;archiviazione MongoDB aggiunge dati a un documento con ogni modifica. Tuttavia, i dati vengono eliminati solo se viene attivata in modo esplicito la pulizia. I vecchi dati vengono spostati quando viene raggiunta una determinata soglia. I documenti precedenti contengono solo dati immutabili, il che significa che contengono solo revisioni salvate e unite.

* Metadati nodo cluster

I dati sui nodi del cluster attivi e inattivi vengono conservati nel database per facilitare le operazioni del cluster.

Configurazione tipica AEM cluster con storage MongoDB:

![chlimage_1-85](assets/chlimage_1-85.png)

## Cos&#39;è diverso da Jackrabbit 2? {#what-is-different-from-jackrabbit}

Poiché Oak è progettato per essere compatibile con lo standard JCR 1.0, non ci saranno quasi modifiche a livello di utente. Tuttavia, durante l&#39;impostazione di un&#39;installazione AEM basata su Oak è necessario tenere conto di alcune differenze notevoli:

* Oak non crea indici automaticamente. Per questo motivo, se necessario, sarà necessario creare indici personalizzati.
* A differenza di Jackrabbit 2, dove le sessioni riflettono sempre lo stato più recente del repository, con Oak una sessione riflette una vista stabile del repository dal momento in cui la sessione è stata acquisita. Ciò è dovuto al modello MVCC su cui si basa Oak.
* Gli stessi nomi di pari livello (SNS) non sono supportati in Oak.

## Documentazione correlata ad altre piattaforme {#other-platform-related-documentation}

Per ulteriori informazioni sulla piattaforma AEM, consultate anche gli articoli seguenti:

* [Configurazione dei nodi e dei data store in AEM 6](/help/sites-deploying/data-store-config.md)
* [Query e indicizzazione Oak](/help/sites-deploying/queries-and-indexing.md)
* [Elementi di storage in AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md)
* [AEM con MongoDB](/help/sites-deploying/aem-with-mongodb.md)

