---
title: Tally Essentials
seo-title: Tally Essentials
description: Panoramica classe conteggio
seo-description: Tally class overview
uuid: c369c6a1-9ced-4b5c-af43-8c03236eaa52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9941ba90-3d40-4c90-bca8-5db49603cbfa
exl-id: 0b508df9-1a24-4728-a254-f913eeb9b391
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Tally Essentials {#tally-essentials}

Tally è una classe astratta che fornisce un metodo standard per raccogliere feedback dai membri su come apprezzano prodotti e servizi specifici. Il feedback anonimo non è supportato. Il visitatore del sito deve registrarsi ed effettuare l&#39;accesso per partecipare ed effettuare l&#39;accesso per modificare i propri commenti. Il requisito di accesso facilita la moderazione e aumenta il valore del feedback impedendo la creazione di più post.

È possibile creare un componente tally personalizzato estendendo la classe tally astratta.

[Mi piace](essentials-liking.md) è un&#39;implementazione del conteggio che è una semplice forma di esprimere un parere positivo.

[Votazione](essentials-voting.md) è un&#39;implementazione di conteggio che è una semplice forma di esprimere un parere positivo o negativo.

[Valutazione](rating-basics.md) è un&#39;implementazione di tally che utilizza un sistema a stella per esprimere una serie di opinioni da positive a negative.

A partire da AEM 6.1, la componente sondaggio non è più disponibile.

[Recensioni](reviews-basics.md) è un componente SCF ibrido di [commenti](essentials-comments.md) e [valutazione](rating-basics.md).

## Nozioni di base per lato client {#essentials-for-client-side}

* [Personalizzazioni lato client](client-customize.md)

## Nozioni di base per lato server {#essentials-for-server-side}

* [API Tally](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Punti finali conteggio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Accesso alle tabelle pubblicate (UGC) {#accessing-posted-tallies-ugc}

Il contenuto UGC deve essere moderato utilizzando uno dei metodi standard per la moderazione.
Consulta [Moderazione dei contenuti generati dagli utenti](moderate-ugc.md).

A partire dalla AEM 6.1 Communities, l&#39;utilizzo di un [archivio comune](working-with-srp.md) per UGC include l’accesso programmatico a UGC indipendentemente dall’opzione di archiviazione scelta (ad esempio ASRP, MSRP o JSRP).

**La posizione e il formato dell’UGC nell’archivio sono soggetti a modifiche senza preavviso**.

Consulta:

* [Panoramica del provider di risorse di archiviazione](srp.md) - Introduzione e panoramica sull’utilizzo dell’archivio.
* [Nozioni di base su SRP e UGC](srp-and-ugc.md) - Metodi ed esempi di utilità SRP.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - Linee guida per la codifica.
* [Refactoring SocialUtils](socialutils.md) - Mappatura dei metodi di utilità obsoleti sui metodi di utilità SRP correnti.
