---
title: Quali ambienti di test sono necessari?
seo-title: Which Test Environments are needed?
description: Diversi ambienti devono essere considerati parte del test
seo-description: Several environments should be considered as part of testing
uuid: bb725e50-edae-4c20-8107-d1c8df2e60e2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# Quali ambienti di test saranno necessari?{#which-test-environments-will-be-needed}

Per definire le configurazioni da testare, prendi in considerazione quanto segue:

**Sviluppo** - Per unit test e alcuni test di integrazione.

**Test** - per la maggior parte dei test.

**Live** - per prove di resistenza e prestazioni finali. Anche per i test di accettazione con il cliente.

Sarà inoltre necessario decidere quali istanze saranno necessarie in cui (in genere almeno una di ciascuna per tutti i livelli di test):

**Autore** : questa istanza consente agli autori di inserire e pubblicare contenuti.

**Pubblica** - Questa istanza presenta il sito web nel modulo pubblicato per l’accesso da parte dei visitatori.

Deve essere testato insieme a Dispatcher.

Infine, è necessario considerare l&#39;hardware effettivo: tutti i test delle prestazioni devono essere eseguiti su un sistema il più vicino possibile all&#39;ambiente live finale. Per questo motivo, si consiglia inoltre di suddividere il lancio del progetto in:

**Lancio morbido** - Disponibilità ridotta, che consente di dedicare tempo ai test delle prestazioni, all&#39;ottimizzazione e al tuning in condizioni realistiche nell&#39;ambiente di produzione.

**Lancio rigido** - Disponibilità completa.
