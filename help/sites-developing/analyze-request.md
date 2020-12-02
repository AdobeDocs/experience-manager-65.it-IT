---
title: Richiedi script di analisi
seo-title: Richiedi script di analisi
description: Lo script di analisi delle richieste consente di semplificare l'analisi dei file access.log, generando un report leggibile per l'elaborazione successiva
seo-description: Lo script di analisi delle richieste consente di semplificare l'analisi dei file access.log, generando un report leggibile per l'elaborazione successiva
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 1%

---


# Request Analysis Script{#request-analysis-script}

## Scarica {#download}

Questo script consente di semplificare l&#39;analisi dei file `access.log` generando un report leggibile per l&#39;elaborazione successiva.

[Ottieni file](assets/analyse-access.sh)

## Descrizione {#description}

Questo script consente di semplificare l&#39;analisi dei file `access.log` generando un report leggibile per l&#39;elaborazione successiva.

Produce il numero complessivo di richieste, GET e POST, la distribuzione delle richieste nel tempo e più.

L&#39;output è in sintassi di Markdown, quindi sarà più semplice convertirlo in PDF con strumenti come pandoc o visualizzarlo in un browser con plug-in come visualizzatore Markdown.

Consente di analizzare un percorso personalizzato fornito sulla riga di comando.

Riprendendo il commento all&#39;interno del file che indica come eseguirlo:

Analizzare CQ `access.log` estrapolando varie informazioni e producendo un output di Markdown su `stdout`.

## Utilizzo {#usage}

`./analyse-access.sh access.log.2013-&ast;`

è possibile fornire percorsi personalizzati aggiuntivi da analizzare sulla riga di comando

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

è possibile salvare l&#39;output con una semplice tubazione

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
