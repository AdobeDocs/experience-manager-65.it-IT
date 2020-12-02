---
title: Forum Essentials
seo-title: Forum Essentials
description: Panoramica del forum
seo-description: Panoramica del forum
uuid: 68849582-8742-40be-9e7e-0b574ae38815
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 059c5bbe-07eb-4873-8157-2196df887b27
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 2%

---


# Forum Essentials {#forum-essentials}

Questa pagina contiene le informazioni essenziali per l’utilizzo della funzione forum.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceTypes</strong></td>
   <td>social/forum/components/hbs/forum<br /> social/forum/components/hbs/topic<br /> social/forum/components/hbs/post</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusa</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.registration<br /> cq.social.hbs.forum</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/forum/components/hbs/forum/forum.hbs<br /> /libs/social/forum/components/hbs/post/post.hbs<br /> /libs/social/forum/components/hbs/topic/topic.hbs<br /> /libs/social/forum/components/hbs/topic/list-item.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/forum/components/hbs/forum/clientlibs/forum.css</td>
  </tr>
  <tr>
   <td><strong> proprietà</strong></td>
   <td>Vedere <a href="forum.md">Funzionalità forum</a></td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API forum](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/forum/client/api/package-summary.html)

* [Endpoint forum](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/forum/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Funzione Forum {#forum-function}

Una struttura del sito della community che include la funzione [Forum](functions.md#forum-function), include un componente `forum` configurato, oltre alle impostazioni relative a moderazione, tag e traduzione.

### Accesso ai post del forum (UGC) {#accessing-forum-posts-ugc}

UGC deve essere moderato utilizzando uno dei metodi standard per la moderazione.
Consultate [Moderazione dei contenuti generati dall&#39;utente](moderate-ugc.md).

A partire da AEM 6.1 Communities, l&#39;utilizzo di un [store comune](working-with-srp.md) per UGC include l&#39;accesso programmatico a UGC indipendentemente dall&#39;opzione di storage scelta (come ASRP, MSRP o JSRP).

**La posizione e il formato dell’UGC nel repository sono soggetti a modifiche senza preavviso**.

Consulta:

* [Panoramica](srp.md)  del provider delle risorse di storage - Introduzione e panoramica sull&#39;utilizzo dell&#39;archivio.
* [SRP e UGC Essentials](srp-and-ugc.md)  - Metodi e esempi di utilità SRP.
* [Accesso a UGC con linee guida SRP](accessing-ugc-with-srp.md) - Codifica.
* [Refactoring](socialutils.md)  SocialUtils - Mappatura di metodi di utilità obsoleti ai metodi di utilità SRP correnti.

