---
title: Voto Essenziali
seo-title: Voto Essenziali
description: Panoramica del componente di voto
seo-description: Panoramica del componente di voto
uuid: ed0a771d-1c14-4fbf-ab6a-a028e5ee2e2a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 1a947a06-6a5c-4be9-b2fa-e5fa809ff3b8
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---


# Voto Essenziali {#voting-essentials}

Il componente Voto, una sottoclasse [tally](tally.md), è uno strumento utile che consente ai membri di valutare un particolare contenuto semplicemente selezionando frecce verso l&#39;alto o il basso per indicare la propria opinione.

È possibile posizionare più istanze di un componente di voto sulla stessa pagina; ogni istanza deve essere configurata con una proprietà `tally name` univoca.

L&#39;invio anonimo di un voto non è supportato. I visitatori del sito devono registrarsi ed effettuare l&#39;accesso per partecipare al voto una sola volta, mentre il visitatore (membro) che ha effettuato l&#39;accesso può modificare il proprio voto in qualsiasi momento.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/components/hbs/Votazione</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusa</strong></a></td>
   <td>Sì - le proprietà sono modificabili in <i>modalità di progettazione </i>modo</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td><p> /libs/social/tally/components/hbs/voting/voting.hbs<br /> /libs/social/tally/components/hbs/voting/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/voting/clientlibs/votingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>proprietà</strong></td>
   <td><p>Vedere <a href="voting.md">Utilizzo del voto</a></p> </td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API Tally](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Endpoint di conteggio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Accesso al Voto Pubblicato (UGC) {#accessing-posted-voting-ugc}

UGC deve essere moderato utilizzando uno dei metodi standard per la moderazione.
Consultate [Moderazione dei contenuti generati dall&#39;utente](moderate-ugc.md).

A partire da AEM 6.1 Communities, l&#39;utilizzo di un [store comune](working-with-srp.md) per UGC include l&#39;accesso programmatico a UGC indipendentemente dall&#39;opzione di storage scelta (come ASRP, MSRP o JSRP).

**La posizione e il formato dell’UGC nel repository sono soggetti a modifiche senza preavviso**.

Consulta:

* [Panoramica](srp.md)  del provider delle risorse di storage - introduzione e panoramica sull&#39;utilizzo dell&#39;archivio.
* [SRP e UGC Essentials](srp-and-ugc.md)  - Metodi e esempi di utilità SRP.
* [Accesso a UGC con linee guida di codifica SRP](accessing-ugc-with-srp.md) .
* [Refactoring](socialutils.md)  SocialUtils: mappatura di metodi di utilità obsoleti ai metodi di utilità SRP correnti.

