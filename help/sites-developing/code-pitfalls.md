---
title: Punteggi dei codici
seo-title: Punteggi dei codici
description: Comuni errori di codifica da evitare durante lo sviluppo per AEM
seo-description: Comuni errori di codifica da evitare durante lo sviluppo per AEM
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Punteggi dei codici{#code-pitfalls}

## Evitare i binding di sling nel codice Java {#avoid-sling-bindings-in-java-code}

I binding Sling sono un modo inappropriato per accedere a un servizio nel 90% dei casi. Utilizzare invece *@Reference* o *@Inject* annotations.

## Evitare Thread.interrupt nel codice Java {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* è pericoloso perché può chiudere i file, inclusi i file Lucene e i file cache persistenti, se richiamati al momento sbagliato.

## Evitare di mixare la sincronizzazione Java con ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Ciò può portare a una condizione di gara in cui il codice si bloccherà alla fine.
