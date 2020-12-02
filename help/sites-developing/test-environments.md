---
title: Quali ambienti di test sono necessari?
seo-title: Quali ambienti di test sono necessari?
description: Diversi ambienti dovrebbero essere considerati parte dei test
seo-description: Diversi ambienti dovrebbero essere considerati parte dei test
uuid: bb725e50-edae-4c20-8107-d1c8df2e60e2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# Quali ambienti di test saranno necessari?{#which-test-environments-will-be-needed}

Per definire le configurazioni da sottoporre a test, è necessario considerare quanto segue:

**Sviluppo**  - Per unità e alcuni test di integrazione.

**Test**  - Per la maggior parte dei test.

**Live**  - Per le prove finali di prestazioni e stress. Anche per i test di accettazione con il cliente.

Sarà inoltre necessario decidere quali istanze sarà necessario dove (in genere almeno uno di ciascuno per tutti i livelli di test):

**Autore** : questa istanza consente agli autori di inserire e pubblicare contenuti.

**Pubblica** : questa istanza presenta il sito Web nel modulo pubblicato per l’accesso dei visitatori.

Deve essere testato insieme al Dispatcher.

Infine, l&#39;hardware vero e proprio deve essere considerato: qualsiasi test di prestazioni dovrebbe essere effettuato su un sistema il più vicino possibile alla configurazione all&#39;ambiente live finale. Per questo motivo, si consiglia anche di suddividere il lancio del progetto in una delle seguenti opzioni:

**Lancio**  morbido - disponibilità ridotta; che consente di eseguire test delle prestazioni, sintonizzazione e ottimizzazione in condizioni realistiche sull&#39;ambiente di produzione.

**Lancio**  rigido - Disponibilità completa.
