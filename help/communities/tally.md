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
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---


# Tally Essentials {#tally-essentials}

Tally è una classe astratta che fornisce un metodo standard per raccogliere i commenti dei membri sul valore di prodotti e servizi specifici. I commenti anonimi non sono supportati. Il visitatore del sito deve registrarsi ed effettuare l&#39;accesso per partecipare ed effettuare l&#39;accesso per cambiare il proprio feedback. Il requisito di accesso facilita la moderazione e migliora il valore del feedback impedendo più post.

È possibile creare un componente personalizzato per il test estendendo la classe astratta tally.

[Il ](essentials-liking.md) Likingè un&#39;attuazione del bilancio che è semplice forma di esprimere un&#39;opinione positiva.

[Il ](essentials-voting.md) voto è un&#39;attuazione del bilancio che è una semplice forma di esprimere un parere positivo o negativo.

[](rating-basics.md) Ratingè un&#39;implementazione di tally che utilizza un sistema a stella per esprimere una serie di opinioni da positive a negative.

A partire dal AEM 6.1, il componente Sondaggio non è più disponibile.

[](reviews-basics.md) Rivedere un componente SCF che è un ibrido di  [](essentials-comments.md) commenti e  [valutazione](rating-basics.md).

## Essentials for Client-Side {#essentials-for-client-side}

* [Personalizzazioni lato client](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API Tally](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Endpoint di conteggio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Accesso alle tabelle pubblicate (UGC) {#accessing-posted-tallies-ugc}

UGC deve essere moderato utilizzando uno dei metodi standard per la moderazione.
Consultate [Moderazione dei contenuti generati dall&#39;utente](moderate-ugc.md).

A partire da AEM 6.1 Communities, l&#39;utilizzo di un [store comune](working-with-srp.md) per UGC include l&#39;accesso programmatico a UGC indipendentemente dall&#39;opzione di storage scelta (come ASRP, MSRP o JSRP).

**La posizione e il formato dell’UGC nel repository sono soggetti a modifiche senza preavviso**.

Consulta:

* [Panoramica](srp.md)  del provider delle risorse di storage - Introduzione e panoramica sull&#39;utilizzo dell&#39;archivio.
* [SRP e UGC Essentials](srp-and-ugc.md)  - Metodi e esempi di utilità SRP.
* [Accesso a UGC con linee guida SRP](accessing-ugc-with-srp.md) - Codifica.
* [Refactoring](socialutils.md)  SocialUtils - Mappatura di metodi di utilità obsoleti ai metodi di utilità SRP correnti.

