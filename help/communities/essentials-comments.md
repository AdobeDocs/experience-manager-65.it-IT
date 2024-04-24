---
title: Commenti essenziali
description: Scopri come utilizzare il sistema di commenti (componente Commenti) e gestire i contenuti generati dagli utenti (UGC) nei post dei membri della community.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8b4034f7-2f97-45ad-96d4-51cfbeae5991
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 4%

---

# Commenti essenziali {#comments-essentials}

Questa pagina fornisce le nozioni di base sull’utilizzo del sistema dei commenti (componente commenti) e le opzioni per la gestione dei contenuti generati dagli utenti (UGC) generati quando i membri pubblicano commenti o risposte.

Il componente commenti stabilisce un sistema di commenti tale che ogni singolo post sia rappresentato da una componente commento (singolare). È il sistema di commenti incluso nella pagina. Il sistema di commenti crea i singoli commenti quando richiamato.

## Nozioni di base per lato client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/commenti</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluso</strong></a></td>
   <td>Sì - le proprietà sono modificabili in <i>progettazione </i>modalità</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>modelli</strong></td>
   <td> /libs/social/commons/components/hbs/comments/comments.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>CSS</strong></td>
   <td> /libs/social/commons/components/hbs/comments/clientlibs/commentsystem.css</td>
  </tr>
  <tr>
   <td><strong> proprietà</strong></td>
   <td> Consulta <a href="comments.md">Utilizzo dei commenti</a></td>
  </tr>
 </tbody>
</table>

[Personalizzazioni lato client](client-customize.md)

### Una Istanza Per Pagina {#one-instance-per-page}

L’impaginazione e l’utilizzo di URL per il caching e il collegamento richiedono che l’URL sia univoco per sistema di commenti. Pertanto, è consentita una sola istanza di un sistema di commenti per pagina.

Altre funzioni includono già il sistema di commenti. Secondo questi principi, il contenuto deve essere:

* [Blog](blog-developer-basics.md)
* [Calendario](calendar-basics-for-developers.md)
* [Libreria file](essentials-file-library.md)
* [Forum](essentials-forum.md)
* [D/R](qna-essentials.md)
* [Recensioni](reviews-basics.md)

### Elenco di motivi per segnalazione {#flag-reason-list}

Per personalizzare l’elenco dei motivi di segnalazione, aggiungi flagreasonlist.hbs all’app per sovrascrivere i contenuti di

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

Ciò si applica a qualsiasi componente che estende un sistema di commenti.

## Nozioni di base per lato server {#essentials-for-server-side}

* [API Commenti](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [Endpoint commenti](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Accesso ai commenti pubblicati (UGC) {#accessing-posted-comments-ugc}

Il contenuto UGC deve essere moderato utilizzando uno dei metodi standard per la moderazione.
Consulta [Moderazione dei contenuti generati dagli utenti](moderate-ugc.md).

A partire dalla AEM 6.1 Communities, l&#39;utilizzo di un [archivio comune](working-with-srp.md) per UGC include l’accesso programmatico a UGC indipendentemente dall’opzione di archiviazione scelta (ad esempio ASRP, MSRP o JSRP).

**La posizione e il formato dell’UGC nell’archivio sono soggetti a modifiche senza preavviso**.

Consulta:

* [Panoramica del provider di risorse di archiviazione](srp.md) - Introduzione e panoramica sull’utilizzo dell’archivio.
* [Nozioni di base su SRP e UGC](srp-and-ugc.md) - Metodi ed esempi di utilità SRP.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - Linee guida per la codifica.
* [Refactoring SocialUtils](socialutils.md) - Mappatura dei metodi di utilità obsoleti sui metodi di utilità SRP correnti.
