---
title: Quali ambienti di test sono necessari?
description: Diversi ambienti devono essere considerati parte del test
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
source-git-commit: 4e2ee7da5424ac6677eaa2392de7803e7543d13c
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Quali ambienti di test sono necessari?{#which-test-environments-will-be-needed}

Per definire le configurazioni da testare, prendi in considerazione quanto segue:

**Sviluppo** - Per unit test e alcuni test di integrazione.

**Test** - Per la maggior parte dei test.

**Live** - per prove di resistenza e prestazioni finali. Anche per i test di accettazione con il cliente.

Decidi quali istanze sono necessarie e dove (in genere almeno una per ogni livello di test):

**Autore** : questa istanza consente agli autori di inserire e pubblicare contenuti.

**Pubblica** - Questa istanza presenta il sito web nel modulo pubblicato per l’accesso da parte dei visitatori.

Testato con Dispatcher.

Infine, è necessario considerare l&#39;hardware effettivo: tutti i test delle prestazioni devono essere eseguiti su un sistema il più vicino possibile all&#39;ambiente live finale. Per questo motivo, si consiglia inoltre di suddividere il lancio del progetto in:

**Lancio morbido** - Disponibilità ridotta, che consente di dedicare tempo ai test delle prestazioni, alla messa a punto e all&#39;ottimizzazione in condizioni realistiche nell&#39;ambiente di produzione.

**Lancio rigido** - Disponibilità completa.
