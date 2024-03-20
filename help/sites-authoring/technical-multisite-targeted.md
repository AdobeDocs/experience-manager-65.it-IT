---
title: Struttura della gestione multisito per contenuti di destinazione
description: Un diagramma mostra come è strutturato il supporto multisito per contenuti mirati
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: d8ba91ff-ad6e-4540-baff-a2c0c764a299
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 38%

---

# Struttura della gestione multisito per contenuti di destinazione{#how-multisite-management-for-targeted-content-is-structured}

Il diagramma seguente mostra come è strutturato il supporto multisito per contenuti di destinazione.

Le aree vengono visualizzate al di sotto di **/content/campaigns/&lt;brand>** e, per impostazione predefinita, ogni marchio ha un’area master che viene creata automaticamente. Ogni area contiene la propria serie di attività, esperienze e offerte.

![chlimage_1-268](assets/chlimage_1-268.png)

Per cercare contenuti mirati, le pagine o i siti possono essere mappati su un’area. Se non è configurata alcuna area, l’AEM torna all’area master per questo marchio specifico.

Il diagramma seguente è un esempio di come funziona la logica per tre siti, denominati site1, site2 e site3.

![chlimage_1-269](assets/chlimage_1-269.png)

* site1 cerca myarea1 per brand1 e otherarea2 per brand2 in base alla mappatura dell’area.
* site2 cerca myarea1 per brand1 e master area per brand2 in quanto viene definita solo la mappatura di area per brand1.
* site3 cerca l’area master per brand1 e brand2 in quanto per questo sito non è definita alcuna altra mappatura di area.
