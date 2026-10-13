---
title: Convenzioni di denominazione per il test delle risorse
description: I nodi nell’archivio sono soggetti alle convenzioni di denominazione dell’archivio dei contenuti Java. Tuttavia, Adobe Experience Manager impone ulteriori convenzioni per il nome dei nodi delle risorse.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: bb6a5913-0871-47c7-8641-936e98920ec0
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 9%
---
# Convenzioni di denominazione per il test delle risorse{#naming-conventions-for-assets-testing}

I nodi dell&#39;archivio sono soggetti alle convenzioni di denominazione dell&#39;[archivio dei contenuti Java](/help/sites-developing/the-basics.md#java-content-repository). Tuttavia, Adobe Experience Manager impone ulteriori convenzioni per il nome dei nodi delle risorse.

## Interfaccia classica {#classic-ui}

L’interfaccia utente classica impone restrizioni più severe:

* Convalida il nome della risorsa quando un nome di nodo esplicito:

  * viene fornito il titolo della risorsa da convertire nel nome del nodo
  * viene fornito un nome di nodo esplicito

* Caratteri validi (solo questi caratteri sono effettivamente validi quando una risorsa viene creata dall’interfaccia classica):

  * Da &#39;a&#39; a &#39;z&#39;
  * Da &#39;A&#39; a &#39;Z&#39;
  * Da &#39;0&#39; a &#39;9&#39;
  * _ (trattino basso)
  * `-` (trattino/segno meno)
