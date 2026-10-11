---
title: Compilazione del piano di test
description: I singoli casi di test sono combinati nel piano di test
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
docset: aem65
exl-id: ee5df2c8-ab31-4be9-8ede-3c96f26fc626
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
source-wordcount: '194'
ht-degree: 4%
---
# Compilazione del piano di test{#compiling-your-test-plan}

I singoli casi di test verranno quindi accorpati nel piano di test, che definirà anche:

**Priorità**

Alcuni test avranno più significato di altri, pertanto è consigliabile indicarne la priorità.

Ad esempio, alcuni test possono influenzare una decisione Go / No-Go, e quindi devono essere confermati con ogni versione provvisoria testata.

**Iterazioni**

Se il progetto utilizza qualsiasi forma di iterazione di sviluppo (che prevede la disponibilità di più versioni), potrebbe essere necessaria o utile un’indicazione dei risultati per ogni iterazione. Può essere utilizzato per indicare:

* quali test verranno inclusi in quale iterazione.
* i risultati osservati per i test ripetuti in varie iterazioni.
* che le prove prioritarie e le prove sulle caratteristiche di base siano ripetute a intervalli regolari.

**Tester**

A un certo punto puoi assegnare il team di test appropriato o una persona di test specifica (possibilmente in base alla disponibilità e/o all’esperienza).

**Riepilogo o panoramica**

A scopo di reporting, è necessario fornire una panoramica dei risultati dei test:

* Percentuale di test già coperti.
* Percentuale di successo/fallimento.
* Dati specifici relativi ai test prioritari.
