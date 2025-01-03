---
title: Tally Essentials
description: Scopri come Tally è una classe astratta che fornisce un metodo standard per raccogliere feedback dai membri su come apprezzano prodotti e servizi specifici.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0b508df9-1a24-4728-a254-f913eeb9b391
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# Tally Essentials {#tally-essentials}

Tally è una classe astratta che fornisce un metodo standard per raccogliere feedback dai membri su come apprezzano prodotti e servizi specifici. Il feedback anonimo non è supportato. I visitatori del sito devono registrarsi ed effettuare l&#39;accesso per partecipare ed effettuare l&#39;accesso per modificare i propri commenti. Il requisito di accesso facilita la moderazione e aumenta il valore del feedback impedendo la creazione di più post.

È possibile creare un componente tally personalizzato estendendo la classe tally astratta.

[Mi piace](essentials-liking.md) è un&#39;implementazione di conteggio che è una semplice forma di esprimere un parere positivo.

[Votare](essentials-voting.md) è un&#39;implementazione del conteggio che è una semplice forma di esprimere un parere positivo o negativo.

[La valutazione](rating-basics.md) è un&#39;implementazione di tally che utilizza un sistema a stella per esprimere una serie di opinioni da positive a negative.

A partire da AEM 6.1, la componente sondaggio non è più disponibile.

[Recensioni](reviews-basics.md) è un componente SCF ibrido di [commenti](essentials-comments.md) e [valutazione](rating-basics.md).

## Nozioni di base per lato client {#essentials-for-client-side}

* [Personalizzazioni lato client](client-customize.md)

## Nozioni di base per lato server {#essentials-for-server-side}

* [API conteggio](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Endpoint conteggio](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Accesso alle tabelle pubblicate (UGC) {#accessing-posted-tallies-ugc}

Il contenuto UGC deve essere moderato utilizzando uno dei metodi standard per la moderazione.
Vedere [Moderazione del contenuto generato dall&#39;utente](moderate-ugc.md).

A partire da AEM 6.1 Communities, l&#39;utilizzo di un [archivio comune](working-with-srp.md) per UGC include l&#39;accesso programmatico a UGC indipendentemente dall&#39;opzione di archiviazione scelta (ad esempio ASRP, MSRP o JSRP).

**La posizione e il formato dell&#39;UGC nell&#39;archivio sono soggetti a modifiche senza preavviso**.

Consulta:

* [Panoramica del provider di risorse di archiviazione](srp.md) - Introduzione e panoramica sull&#39;utilizzo dell&#39;archivio.
* [SRP e UGC Essentials](srp-and-ugc.md) - Metodi ed esempi dell&#39;utilità SRP.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - Linee guida per la codifica.
* [Refactoring di SocialUtils](socialutils.md) - Mappatura dei metodi di utilità obsoleti ai metodi di utilità SRP correnti.
