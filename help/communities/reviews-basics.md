---
title: Elementi di base recensioni
description: Scopri come Reviews in AEM Communities è un componente composito basato su un sistema di commenti che contiene uno o più componenti di valutazione (tally).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 1%

---

# Elementi di base recensioni {#reviews-essentials}

Questa funzione è costituita da due componenti che lavorano insieme: revisioni e riepilogo delle revisioni.

Recensioni è un componente composito basato su un [sistema di commenti](essentials-comments.md) che contiene uno o più componenti [valutazione](rating-basics.md) (conteggio).

La pubblicazione anonima di una revisione non è supportata. Per aggiungere una recensione, i visitatori del sito devono registrarsi e accedere. Il visitatore (membro) che ha effettuato l’accesso può aggiornare la propria revisione in qualsiasi momento.

## Nozioni di base per lato client {#essentials-for-client-side}

### Recensioni {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>tiporisorsa</strong></td>
   <td>social/recensioni/componenti/hbs/recensioni</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>includibile</strong></a></td>
   <td>Sì - le proprietà sono modificabili in modalità <i>progettazione </i></td>
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
   <td>Vedi <a href="reviews.md">Utilizzo delle recensioni</a></td>
  </tr>
 </tbody>
</table>

### Riepilogo recensioni {#review-summary}

| **tiporisorsa** | social/recensioni/componenti/hbs/riepilogo |
|---|---|
| [**includibile**](scf.md#add-or-include-a-communities-component) | Sì - le proprietà sono modificabili nel modo *design * |
| [**clientllibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **modelli** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **proprietà** | Vedi [Utilizzo delle recensioni](reviews.md) |

* [Personalizzazioni lato client](client-customize.md)

## Nozioni di base per lato server {#essentials-for-server-side}

* [Rivedi API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [Endpoint revisione](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Accesso alle recensioni postate (UGC) {#accessing-posted-reviews-ugc}

Il contenuto UGC deve essere moderato utilizzando uno dei metodi standard per la moderazione.
Vedere [Moderazione del contenuto generato dall&#39;utente](moderate-ugc.md).

A partire da AEM 6.1 Communities, l&#39;utilizzo di un [archivio comune](working-with-srp.md) per UGC include l&#39;accesso programmatico a UGC indipendentemente dall&#39;opzione di archiviazione scelta (ad esempio ASRP, MSRP o JSRP).

**La posizione e il formato dell&#39;UGC nell&#39;archivio sono soggetti a modifiche senza preavviso**.

Consulta:

* [Panoramica del provider di risorse di archiviazione](srp.md) - Introduzione e panoramica sull&#39;utilizzo dell&#39;archivio.
* [SRP e UGC Essentials](srp-and-ugc.md) - Metodi ed esempi dell&#39;utilità SRP.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - Linee guida per la codifica.
* [Refactoring di SocialUtils](socialutils.md) - Mappatura dei metodi di utilità obsoleti ai metodi di utilità SRP correnti.
