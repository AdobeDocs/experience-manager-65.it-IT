---
title: Nozioni di base sulla valutazione
seo-title: Rating Essentials
description: Panoramica del componente Valutazione
seo-description: Rating component overview
uuid: 48ef61ad-be7a-4a6b-a284-23e5bb4f1671
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 7dc3ef57-05c3-45d4-ace3-bb3ba6ea768b
exl-id: 49456944-ff0d-4507-b3b8-143c90067573
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 1%

---

# Nozioni di base sulla valutazione {#rating-essentials}

Il componente di valutazione, un [conteggio](tally.md) sottoclasse, consente ai membri della community con accesso effettuato di assegnare una valutazione a una funzione del sito web.

È consentito posizionare più istanze di un componente voting sulla stessa pagina; ogni istanza deve essere configurata con un `tally name` proprietà.

La pubblicazione anonima di una valutazione non è supportata. I visitatori del sito devono registrarsi e accedere per partecipare a una valutazione una sola volta. Il visitatore con accesso (membro) può modificare la propria valutazione in qualsiasi momento.

## Nozioni di base per lato client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/tally/components/hbs/rating</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluso</strong></a></td>
   <td>Sì - le proprietà sono modificabili in <i>progettazione </i>modalità</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.rating</td>
  </tr>
  <tr>
   <td> <strong>modelli</strong></td>
   <td><p> /libs/social/tally/components/hbs/rating/rating.hbs<br /> /libs/social/tally/components/hbs/rating/display.hbs<br /> /libs/social/tally/components/hbs/rating/histogram.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/rating/clientlibs/ratingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>proprietà</strong></td>
   <td><p>Consulta <a href="rating.md">Utilizzo della valutazione</a></p> </td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](client-customize.md)

## Nozioni di base per lato server {#essentials-for-server-side}

* [API Tally](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Punti finali conteggio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Accesso alle valutazioni pubblicate (UGC) {#accessing-posted-ratings-ugc}

Il contenuto UGC deve essere moderato utilizzando uno dei metodi standard per la moderazione.
Consulta [Moderazione dei contenuti generati dagli utenti](moderate-ugc.md).

A partire dalla AEM 6.1 Communities, l&#39;utilizzo di un [archivio comune](working-with-srp.md) per UGC include l’accesso programmatico a UGC indipendentemente dall’opzione di archiviazione scelta (ad esempio ASRP, MSRP o JSRP).

**La posizione e il formato dell’UGC nell’archivio sono soggetti a modifiche senza preavviso**.

Consulta:

* [Panoramica del provider di risorse di archiviazione](srp.md) - introduzione e panoramica sull’utilizzo dell’archivio.
* [Nozioni di base su SRP e UGC](srp-and-ugc.md) - Metodi ed esempi di utilità SRP.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - linee guida per la codifica.
* [Refactoring SocialUtils](socialutils.md) - mappatura dei metodi di utilità obsoleti sui metodi di utilità SRP correnti.
