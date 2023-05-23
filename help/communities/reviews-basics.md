---
title: Elementi di base recensioni
seo-title: Reviews Essentials
description: Revisioni e componenti Riepilogo recensioni
seo-description: Reviews and Review Summary components
uuid: 540c106e-ee3b-4261-82b2-a909d254dbf7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 62669a9d-2107-4644-a4bf-143d0ac148b3
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 1%

---

# Elementi di base recensioni {#reviews-essentials}

Questa funzione è costituita da due componenti che lavorano insieme: revisioni e riepilogo delle revisioni.

Recensioni è un componente composito basato su una [sistema di commenti](essentials-comments.md) che contiene uno o più [valutazione](rating-basics.md) Componenti (tally).

La pubblicazione anonima di una revisione non è supportata. Per aggiungere una recensione, i visitatori del sito devono registrarsi e accedere. Il visitatore (membro) che ha effettuato l’accesso può aggiornare la propria revisione in qualsiasi momento.

## Nozioni di base per lato client {#essentials-for-client-side}

### Recensioni {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/recensioni/componenti/hbs/recensioni</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluso</strong></a></td>
   <td>Sì - le proprietà sono modificabili in <i>progettazione </i>modalità</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.reviews</td>
  </tr>
  <tr>
   <td> <strong>modelli</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/reviews.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/review.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/status.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/toolbar.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/clientlibs/review.css</td>
  </tr>
  <tr>
   <td><strong>proprietà</strong></td>
   <td>Consulta <a href="reviews.md">Utilizzo delle revisioni</a></td>
  </tr>
 </tbody>
</table>

### Riepilogo recensioni {#review-summary}

| **resourceType** | social/recensioni/componenti/hbs/riepilogo |
|---|---|
| [**incluso**](scf.md#add-or-include-a-communities-component) | Sì - le proprietà sono modificabili nel modo *design * |
| [**clientllibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **modelli** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **proprietà** | Consulta [Utilizzo delle revisioni](reviews.md) |

* [Personalizzazioni lato client](client-customize.md)

## Nozioni di base per lato server {#essentials-for-server-side}

* [API di revisione](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [Endpoint di revisione](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Accesso alle recensioni postate (UGC) {#accessing-posted-reviews-ugc}

Il contenuto UGC deve essere moderato utilizzando uno dei metodi standard per la moderazione.
Consulta [Moderazione dei contenuti generati dagli utenti](moderate-ugc.md).

A partire dalla AEM 6.1 Communities, l&#39;utilizzo di un [archivio comune](working-with-srp.md) per UGC include l’accesso programmatico a UGC indipendentemente dall’opzione di archiviazione scelta (ad esempio ASRP, MSRP o JSRP).

**La posizione e il formato dell’UGC nell’archivio sono soggetti a modifiche senza preavviso**.

Consulta:

* [Panoramica del provider di risorse di archiviazione](srp.md) - Introduzione e panoramica sull’utilizzo dell’archivio.
* [Nozioni di base su SRP e UGC](srp-and-ugc.md) - Metodi ed esempi di utilità SRP.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - Linee guida per la codifica.
* [Refactoring SocialUtils](socialutils.md) - Mappatura dei metodi di utilità obsoleti sui metodi di utilità SRP correnti.
