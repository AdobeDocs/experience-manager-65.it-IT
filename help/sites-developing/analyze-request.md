---
title: Script di analisi delle richieste
seo-title: Request Analysis Script
description: Lo script di analisi della richiesta viene eseguito per facilitare l'analisi dei file access.log producendo un report leggibile per l'elaborazione successiva
seo-description: The request analysis script is made to ease the analysis of the access.log files producing a readable report for later processing
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
exl-id: e14a9cda-890f-46b7-9433-1b52eb91eae3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# Script di analisi delle richieste{#request-analysis-script}

## Scarica {#download}

Questo script è fatto per facilitare l&#39;analisi del `access.log` file che producono un rapporto leggibile per un&#39;elaborazione successiva.

[Ottieni file](assets/analyse-access.sh)

## Descrizione {#description}

Questo script è fatto per facilitare l&#39;analisi del `access.log` file che producono un rapporto leggibile per un&#39;elaborazione successiva.

Produce il numero complessivo di richieste, GET vs POST, Distribuzione delle richieste nel tempo e molto altro.

L’output è in sintassi Markdown e sarà quindi più facile convertirlo in PDF con strumenti come pandoc o mostrarlo in un browser con plug-in come visualizzatore Markdown.

Consente di analizzare un percorso personalizzato fornito sulla riga di comando.

Prendendo dal commento all&#39;interno del file che ti dice come eseguirlo:

Analizza CQ `access.log` estrapolazione di varie informazioni e produzione di un output Markdown su `stdout`.

## Utilizzo {#usage}

`./analyse-access.sh access.log.2013-&ast;`

puoi fornire percorsi personalizzati aggiuntivi da analizzare sulla riga di comando

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

è possibile salvare l&#39;output con una semplice tubazione

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
