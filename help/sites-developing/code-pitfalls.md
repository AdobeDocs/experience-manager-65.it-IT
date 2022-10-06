---
title: Problemi di codice
seo-title: Code pitfalls
description: Problemi comuni di codifica da evitare durante lo sviluppo per AEM
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

# Problemi di codice{#code-pitfalls}

## Evitare i binding Sling nel codice Java {#avoid-sling-bindings-in-java-code}

I binding Sling sono un modo inappropriato per accedere a un servizio nel 90% dei casi. Invece, devi utilizzare *@Reference* o *@Inject* annotazioni.

## Evita Thread.interrupt nel codice Java {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* è pericoloso perché può chiudere i file, inclusi i file Lucene e i file di cache persistenti, quando vengono chiamati al momento sbagliato.

## Evita di mixare la sincronizzazione Java con ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Questo può portare a una condizione di corsa in cui il codice alla fine si bloccherà.
