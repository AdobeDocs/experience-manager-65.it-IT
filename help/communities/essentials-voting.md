---
title: Elementi essenziali del voto
seo-title: Voting Essentials
description: Panoramica del componente Voto
seo-description: Voting component overview
uuid: ed0a771d-1c14-4fbf-ab6a-a028e5ee2e2a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 1a947a06-6a5c-4be9-b2fa-e5fa809ff3b8
exl-id: e8ff751f-404a-498d-8e90-62a13ab593ff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# Elementi essenziali del voto {#voting-essentials}

la componente di voto, [tally](tally.md) subclass, è uno strumento utile che consente ai membri di valutare un particolare contenuto semplicemente selezionando frecce verso l’alto o il basso per indicare la propria opinione.

È consentito posizionare più istanze di un componente con diritto di voto sulla stessa pagina; ogni istanza deve essere configurata con un `tally name` proprietà.

L&#39;invio anonimo di un voto non è supportato. I visitatori del sito devono registrarsi e accedere per partecipare al voto una sola volta, il visitatore (membro) che ha effettuato l&#39;accesso può modificare il proprio voto in qualsiasi momento.

## Funzionalità di base per lato client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/components/hbs/vote</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>comprensivo</strong></a></td>
   <td>Sì - le proprietà sono modificabili in <i>progettazione </i>modalità</td>
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
   <td><p>Vedi <a href="voting.md">Utilizzo del voto</a></p> </td>
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
