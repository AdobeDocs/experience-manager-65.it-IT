---
title: Nozioni di base sulla valutazione
description: Scopri in che modo il componente Valutazione, una sottoclasse Tally, consente ai membri della community con accesso effettuato di valutare una funzione sul sito web.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 49456944-ff0d-4507-b3b8-143c90067573
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# Nozioni di base sulla valutazione {#rating-essentials}

Il componente di valutazione, una sottoclasse [tally](tally.md), consente ai membri della community con accesso esterno di valutare una funzionalità del sito Web.

È consentito inserire più istanze di un componente voting nella stessa pagina; ogni istanza deve essere configurata con una proprietà `tally name` univoca.

La pubblicazione anonima di una valutazione non è supportata. I visitatori del sito devono registrarsi e accedere per partecipare a una valutazione una sola volta. Il visitatore con accesso (membro) può modificare la propria valutazione in qualsiasi momento.

## Nozioni di base per lato client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>tiporisorsa</strong></td>
   <td> social/tally/components/hbs/rating</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>includibile</strong></a></td>
   <td>Sì - le proprietà sono modificabili in modalità <i>progettazione </i></td>
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
   <td><p>Vedi <a href="rating.md">Utilizzo della valutazione</a></p> </td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](client-customize.md)

## Nozioni di base per lato server {#essentials-for-server-side}

* [API conteggio](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Endpoint conteggio](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Accesso alle valutazioni pubblicate (UGC) {#accessing-posted-ratings-ugc}

Il contenuto UGC deve essere moderato utilizzando uno dei metodi standard per la moderazione.
Vedere [Moderazione del contenuto generato dall&#39;utente](moderate-ugc.md).

A partire da AEM 6.1 Communities, l&#39;utilizzo di un [archivio comune](working-with-srp.md) per UGC include l&#39;accesso programmatico a UGC indipendentemente dall&#39;opzione di archiviazione scelta (ad esempio ASRP, MSRP o JSRP).

**La posizione e il formato dell&#39;UGC nell&#39;archivio sono soggetti a modifiche senza preavviso**.

Consulta:

* [Panoramica del provider di risorse di archiviazione](srp.md) - introduzione e panoramica sull&#39;utilizzo dell&#39;archivio.
* [SRP e UGC Essentials](srp-and-ugc.md) - Metodi ed esempi dell&#39;utilità SRP.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - linee guida per la codifica.
* [Refactoring di SocialUtils](socialutils.md) - mapping dei metodi di utilità obsoleti ai metodi di utilità SRP correnti.
