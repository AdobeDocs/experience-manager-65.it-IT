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
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

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
