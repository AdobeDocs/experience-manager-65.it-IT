---
title: Struttura della gestione multisito per contenuti di destinazione
seo-title: Struttura della gestione multisito per contenuti di destinazione
description: Un diagramma illustra il modo in cui è strutturato il supporto multisito per contenuti di destinazione
seo-description: Un diagramma illustra il modo in cui è strutturato il supporto multisito per contenuti di destinazione
uuid: 2d30cdf0-ab77-490d-aac0-db3a0d417a58
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 7dd851ab-3fa7-426e-89cb-08b67e9b5999
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 90%

---


# Struttura della gestione multisito per contenuti di destinazione{#how-multisite-management-for-targeted-content-is-structured}

Il diagramma seguente illustra il modo in cui è strutturato il supporto multisito per contenuti di destinazione.

Le aree vengono visualizzate sotto **/content/campaign/&lt;brand>** e per impostazione predefinita ogni marchio ha un&#39;area master, che viene creata automaticamente. Ogni area contiene la propria serie di attività, esperienze e offerte.

![chlimage_1-268](assets/chlimage_1-268.png)

Per cercare contenuti di destinazione, le pagine o i siti possono essere associati a un&#39;area. Se non è presente alcuna area configurata, AEM torna indietro all&#39;area master per questo marchio specifico.

Il diagramma seguente è un esempio di come funziona la logica per tre siti, denominati site1, site2 e site3.

![chlimage_1-269](assets/chlimage_1-269.png)

* site1 cerca myarea1 per brand1 e otherarea2 per brand2 in base alla mappatura dell&#39;area.
* site2 cerca myarea1 per brand1 e l&#39;area master per brand2 perché è definita solo la mappatura dell&#39;area per brand1.
* site3 cerca l&#39;area master per brand1 e brand2 in quanto nessun&#39;altra area di mappatura è definita per questo sito.

