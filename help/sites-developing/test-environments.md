---
title: Quali ambienti di test sono necessari?
description: Diversi ambienti devono essere considerati parte del test
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 5%
---
# Quali ambienti di test sono necessari?{#which-test-environments-will-be-needed}

Per definire le configurazioni da testare, prendi in considerazione quanto segue:

**Sviluppo** - Per unit test e alcuni Integration test.

**Test** - Per la maggior parte dei test.

**Live** - Per le prestazioni finali e gli stress test. Anche per i test di accettazione con il cliente.

Decidi quali istanze sono necessarie e dove (in genere almeno una per ogni livello di test):

**Autore** - Questa istanza consente agli autori di inserire e pubblicare contenuti.

**Pubblicazione** - Questa istanza presenta il sito Web nel relativo modulo pubblicato per l&#39;accesso da parte dei visitatori.

Testato con Dispatcher.

Infine, è necessario considerare l&#39;hardware effettivo: tutti i test delle prestazioni devono essere eseguiti su un sistema il più vicino possibile all&#39;ambiente live finale. Per questo motivo, si consiglia inoltre di suddividere il lancio del progetto in:

**Lancio morbido** - Disponibilità ridotta, che consente di eseguire test delle prestazioni, ottimizzare e ottimizzare in condizioni realistiche l&#39;ambiente di produzione.

**Lancio rigido** - Disponibilità completa.
