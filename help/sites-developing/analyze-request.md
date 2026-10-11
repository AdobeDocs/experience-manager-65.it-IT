---
title: Richiedere lo script di analisi
description: Lo script di analisi delle richieste viene eseguito per semplificare l’analisi dei file access.log e produrre un rapporto leggibile per l’elaborazione successiva
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: e14a9cda-890f-46b7-9433-1b52eb91eae3
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
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 6%
---
# Richiedere lo script di analisi{#request-analysis-script}

## Scarica {#download}

Questo script è stato creato per semplificare l&#39;analisi dei file `access.log` producendo un report leggibile per l&#39;elaborazione successiva.

[Ottieni il file](assets/analyse-access.sh)

## Descrizione {#description}

Questo script è stato creato per semplificare l&#39;analisi dei file `access.log` producendo un report leggibile per l&#39;elaborazione successiva.

Genera il numero complessivo di richieste, GET vs POST, Distribuzione delle richieste nel tempo e altro ancora.

L’output è in sintassi Markdown, pertanto sarà più semplice convertirlo in PDF con strumenti come pandoc o mostrarlo in un browser con plug-in come Markdown viewer.

Può analizzare un percorso personalizzato fornito sulla riga di comando.

Prendendo spunto dal commento all’interno del file che ti spiega come eseguirlo:

Analizzare CQ `access.log` estrapolando varie informazioni e generando un output Markdown su `stdout`.

## Utilizzo {#usage}

`./analyse-access.sh access.log.2013-&ast;`

puoi fornire percorsi personalizzati aggiuntivi da analizzare sulla riga di comando

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

potete salvare l&#39;output mediante una semplice tubazione

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
