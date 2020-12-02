---
title: Punteggi dei codici
seo-title: Punteggi dei codici
description: Comuni errori di codifica da evitare quando si sviluppano per AEM
seo-description: Comuni errori di codifica da evitare quando si sviluppano per AEM
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---


# Problemi di codice{#code-pitfalls}

## Evitare i binding Sling nel codice Java {#avoid-sling-bindings-in-java-code}

I binding Sling sono un modo inappropriato per accedere a un servizio nel 90% dei casi. Utilizzare invece le annotazioni *@Reference* o *@Inject*.

## Evitare Thread.interrupt nel codice Java {#avoid-thread-interrupt-in-java-code}

*Thread.* interruptis pericolosa perché può chiudere i file, inclusi i file Lucene e i file cache persistenti, quando chiamato al momento sbagliato.

## Evitare di mescolare la sincronizzazione Java con ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Ciò può portare a una condizione di gara in cui il codice si bloccherà alla fine.
