---
title: Insidie del codice
description: Insidie di codifica comuni da evitare durante lo sviluppo per l’AEM
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Insidie del codice{#code-pitfalls}

## Evitare le associazioni Sling nel codice Java {#avoid-sling-bindings-in-java-code}

Le associazioni Sling rappresentano un modo inappropriato per accedere a un servizio nel 90% dei casi. Al loro posto, utilizza *@Reference* o *@Inject* annotazioni.

## Evitare Thread.interrupt nel codice Java {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* è pericoloso perché può chiudere i file, inclusi i file Lucene e i file di cache persistenti, quando vengono chiamati al momento sbagliato.

## Evitare di combinare la sincronizzazione Java con ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Questo può portare a una situazione di tipo &quot;race condition&quot; in cui il codice alla fine si blocca.
