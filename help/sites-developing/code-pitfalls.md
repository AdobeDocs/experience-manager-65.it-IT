---
title: Insidie del codice
seo-title: Code pitfalls
description: Insidie di codifica comuni da evitare durante lo sviluppo per l’AEM
seo-description: Common coding pitfalls to avoid when developing for AEM
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Insidie del codice{#code-pitfalls}

## Evitare le associazioni Sling nel codice Java {#avoid-sling-bindings-in-java-code}

Le associazioni Sling rappresentano un modo inappropriato per accedere a un servizio nel 90% dei casi. Al loro posto, utilizza *@Reference* o *@Inject* annotazioni.

## Evitare Thread.interrupt nel codice Java {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* è pericoloso perché può chiudere i file, inclusi i file Lucene e i file di cache persistenti, quando vengono chiamati al momento sbagliato.

## Evitare di combinare la sincronizzazione Java con ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Questo può portare a una situazione di tipo &quot;race condition&quot; in cui il codice alla fine si blocca.
