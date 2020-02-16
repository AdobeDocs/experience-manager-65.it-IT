---
title: Recensioni Essentials
seo-title: Recensioni Essentials
description: Revisioni e revisione dei componenti di riepilogo
seo-description: Revisioni e revisione dei componenti di riepilogo
uuid: 540c106e-ee3b-4261-82b2-a909d254dbf7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 62669a9d-2107-4644-a4bf-143d0ac148b3
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Recensioni Essentials {#reviews-essentials}

Questa funzione è composta da due componenti che funzionano insieme: revisione e riepilogo della revisione.

Revisioni è un componente composito basato su un sistema [di](essentials-comments.md) commenti che contiene uno o più componenti di [valutazione](rating-basics.md) (tally).

L&#39;invio anonimo di una revisione non è supportato. I visitatori del sito devono registrarsi ed effettuare l&#39;accesso per aggiungere una revisione. Il visitatore che ha effettuato l’accesso (membro) può aggiornare la propria revisione in qualsiasi momento.

## Essentials for Client-Side {#essentials-for-client-side}

### Recensioni {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/review/components/hbs/review</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusa</strong></a></td>
   <td>Sì - le proprietà sono modificabili in <i>modalità </i>di progettazione</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.recensioni</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/reviews.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/review.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/status.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/toolbar.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/clientlibs/review.css</td>
  </tr>
  <tr>
   <td><strong>proprietà</strong></td>
   <td>Vedere <a href="reviews.md">Utilizzo delle revisioni</a></td>
  </tr>
 </tbody>
</table>

### Riepilogo recensioni {#review-summary}

| **resourceType** | social/review/components/hbs/summary |
|---|---|
| [**inclusa **](scf.md#add-or-include-a-communities-component) | Sì - le proprietà sono modificabili nel *design *mode |
| [**clientllibs **](client-customize.md#clientlibs-for-scf) | cq.social.hbs.recensioni |
| **templates** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **proprietà** | Vedere [Utilizzo delle revisioni](reviews.md) |

* [Personalizzazioni lato client](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API Review](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [Rivedi endpoint](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Accesso a revisioni registrate (UGC) {#accessing-posted-reviews-ugc}

UGC deve essere moderato utilizzando uno dei metodi standard per la moderazione.
Consultate [Moderazione del contenuto](moderate-ugc.md)generato dall&#39;utente.

A partire da AEM 6.1 Communities, l’utilizzo di uno store [](working-with-srp.md) comune per UGC include l’accesso programmatico a UGC, indipendentemente dall’opzione di archiviazione scelta (come ASRP, MSRP o JSRP).

**La posizione e il formato dell’UGC nel repository sono soggetti a modifiche senza preavviso**.

Vedi:

* [Panoramica](srp.md) del provider di risorse di storage - introduzione e utilizzo del repository
* [Caratteristiche essenziali di SRP e UGC](srp-and-ugc.md) - Metodi e esempi di utilità SRP
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - linee guida di codifica
* [Refactoring](socialutils.md) SocialUtils - mappatura di metodi di utilità obsoleti ai metodi di utilità SRP correnti

