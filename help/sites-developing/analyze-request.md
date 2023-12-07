---
title: Richiedi script di analisi
description: Lo script di analisi delle richieste viene eseguito per semplificare l’analisi dei file access.log e produrre un rapporto leggibile per l’elaborazione successiva
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: e14a9cda-890f-46b7-9433-1b52eb91eae3
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# Richiedi script di analisi{#request-analysis-script}

## Scarica {#download}

Questo script è stato creato per facilitare l&#39;analisi del `access.log` file che generano un rapporto leggibile per l’elaborazione successiva.

[Ottieni file](assets/analyse-access.sh)

## Descrizione {#description}

Questo script è stato creato per facilitare l&#39;analisi del `access.log` file che generano un rapporto leggibile per l’elaborazione successiva.

Genera il numero complessivo di richieste, GET rispetto a POST, Distribuzione delle richieste nel tempo e altro ancora.

L’output è in sintassi Markdown, pertanto sarà più semplice convertirlo in PDF con strumenti come pandoc o mostrarlo in un browser con plug-in come Markdown viewer.

Può analizzare un percorso personalizzato fornito sulla riga di comando.

Prendendo spunto dal commento all’interno del file che ti spiega come eseguirlo:

Analizza CQ `access.log` estrapolare varie informazioni e produrre un output Markdown su `stdout`.

## Utilizzo {#usage}

`./analyse-access.sh access.log.2013-&ast;`

puoi fornire percorsi personalizzati aggiuntivi da analizzare sulla riga di comando

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

potete salvare l&#39;output mediante una semplice tubazione

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
