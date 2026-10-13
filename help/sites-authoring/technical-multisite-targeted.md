---
title: Struttura della gestione multisito per contenuti di destinazione
description: Un diagramma mostra come è strutturato il supporto multisito per contenuti mirati
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: d8ba91ff-ad6e-4540-baff-a2c0c764a299
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
  - id: eb3ad9f8-54a2-45f3-abb1-d3976415a718
    internal-label: Personalization
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 38%
---
# Struttura della gestione multisito per contenuti di destinazione{#how-multisite-management-for-targeted-content-is-structured}

Il diagramma seguente mostra come è strutturato il supporto multisito per contenuti di destinazione.

Le aree vengono visualizzate al di sotto di **/content/campaigns/&lt;brand>** e, per impostazione predefinita, ogni marchio ha un’area master che viene creata automaticamente. Ogni area contiene la propria serie di attività, esperienze e offerte.

![chlimage_1-268](assets/chlimage_1-268.png)

Per cercare contenuti mirati, le pagine o i siti possono essere mappati su un’area. Se non è configurata alcuna area, AEM torna all’area master per questo marchio specifico.

Il diagramma seguente è un esempio di come funziona la logica per tre siti, denominati site1, site2 e site3.

![chlimage_1-269](assets/chlimage_1-269.png)

* site1 cerca myarea1 per brand1 e otherarea2 per brand2 in base alla mappatura dell’area.
* site2 cerca myarea1 per brand1 e master area per brand2 in quanto viene definita solo la mappatura di area per brand1.
* site3 cerca l’area master per brand1 e brand2 in quanto per questo sito non è definita alcuna altra mappatura di area.
