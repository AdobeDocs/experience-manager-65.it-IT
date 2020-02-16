---
title: Tally Essentials
seo-title: Tally Essentials
description: Panoramica della classe Tally
seo-description: Panoramica della classe Tally
uuid: c369c6a1-9ced-4b5c-af43-8c03236eaa52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9941ba90-3d40-4c90-bca8-5db49603cbfa
translation-type: tm+mt
source-git-commit: 9532c1fb8af37b29285007bc72e86d42d5eb9c4d

---


# Tally Essentials {#tally-essentials}

Tally è una classe astratta che fornisce un metodo standard per raccogliere i commenti dei membri sul valore di prodotti e servizi specifici. I commenti anonimi non sono supportati. Il visitatore del sito deve registrarsi ed effettuare l&#39;accesso per partecipare e accedere per cambiare il proprio feedback. Il requisito di accesso facilita la moderazione e migliora il valore del feedback impedendo più post.

È possibile creare un componente personalizzato per il test estendendo la classe astratta tally.

[Il piacere](essentials-liking.md) è un&#39;attuazione del bilancio che è semplice forma di esprimere un parere positivo.

[Votare](essentials-voting.md) è un&#39;attuazione del bilancio che è una semplice forma di esprimere un parere positivo o negativo.

[La valutazione](rating-basics.md) è un&#39;implementazione di tally che utilizza un sistema a stella per esprimere una serie di opinioni da positive a negative.

A partire da AEM 6.1, il componente [sondaggio](poll-basics.md) non è più disponibile.

[Revisioni](reviews-basics.md) è un componente SCF ibrido di [commenti](essentials-comments.md) e [valutazioni](rating-basics.md).

## Essentials for Client-Side {#essentials-for-client-side}

* [Personalizzazioni lato client](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API Tally](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Endpoint di conteggio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Accesso a tabelle pubblicate (UGC) {#accessing-posted-tallies-ugc}

UGC deve essere moderato utilizzando uno dei metodi standard per la moderazione.
Consultate [Moderazione del contenuto](moderate-ugc.md)generato dall&#39;utente.

A partire da AEM 6.1 Communities, l’utilizzo di uno store [](working-with-srp.md) comune per UGC include l’accesso programmatico a UGC, indipendentemente dall’opzione di archiviazione scelta (come ASRP, MSRP o JSRP).

**La posizione e il formato dell’UGC nel repository sono soggetti a modifiche senza preavviso**.

Vedi:

* [Panoramica](srp.md) del provider di risorse di storage - introduzione e utilizzo del repository
* [Caratteristiche essenziali di SRP e UGC](srp-and-ugc.md) - Metodi e esempi di utilità SRP
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - linee guida di codifica
* [Refactoring](socialutils.md) SocialUtils - mappatura di metodi di utilità obsoleti ai metodi di utilità SRP correnti

