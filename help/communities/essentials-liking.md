---
title: Nozioni di base
seo-title: Liking Essentials
description: Panoramica dei componenti Mi piace
seo-description: Liking component overview
uuid: 89f16859-c901-4090-8e16-363b95c508de
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f176c42b-b16b-42c9-af22-4b6421de5a90
pagetitle: Liking Essentials
exl-id: ef314385-cd5c-411c-91df-83691a81c1bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 1%

---

# Nozioni di base {#liking-essentials}

Il componente di collegamento, un [tally](tally.md) subclass, è uno strumento utile che permette ai membri di esprimere un parere positivo su un particolare contenuto semplicemente selezionando l&#39;icona del cuore.

È consentito posizionare più istanze di un componente di collegamento sulla stessa pagina; ogni istanza deve essere configurata con un `tally name` proprietà.

Pubblicazione anonima di un simile non supportata. I visitatori del sito devono registrarsi e accedere per partecipare. Il visitatore con accesso (membro) può attivare e disattivare i parametri in qualsiasi momento.

## Funzionalità di base per lato client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/components/hbs/Mi piace</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>comprensivo</strong></a></td>
   <td>Sì - le proprietà sono modificabili in <i>progettazione </i>modalità</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.liking</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td><p> /libs/social/tally/components/hbs/liking/liking.hbs<br /> /libs/social/tally/components/hbs/liking/activity-icon.hbs<br /> /libs/social/tally/components/hbs/liking/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/liking/clientlibs/likingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>proprietà</strong></td>
   <td><p>Vedi <a href="liking.md">Utilizzo del collegamento</a></p> </td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](client-customize.md)

## Funzioni di base per lato server {#essentials-for-server-side}

* [API Tally](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Endpoint tally](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Accesso al voto postato (UGC) {#accessing-posted-voting-ugc}

UGC dovrebbe essere moderato utilizzando uno dei metodi standard per la moderazione.
Vedi [Moderazione dei contenuti generati dagli utenti](moderate-ugc.md).

A partire da AEM 6.1 Comunità, l&#39;uso di un [negozio comune](working-with-srp.md) per UGC include l&#39;accesso programmatico a UGC indipendentemente dall&#39;opzione di archiviazione scelta (come ASRP, MSRP o JSRP).

**La posizione e il formato dell’UGC nell’archivio sono soggetti a modifiche senza preavviso**.

Consulta:

* [Panoramica del provider di risorse di storage](srp.md) - introduzione e panoramica sull’utilizzo dell’archivio.
* [Essenze SRP e UGC](srp-and-ugc.md) - Metodi ed esempi di utilità SRP.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - linee guida per la codifica.
* [Refactoring di SocialUtils](socialutils.md) - mappatura di metodi di utilità obsoleti ai metodi di utilità SRP correnti.
