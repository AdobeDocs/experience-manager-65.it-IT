---
title: Nozioni di base sui forum
seo-title: Forum Essentials
description: Panoramica del forum
seo-description: Forum overview
uuid: 68849582-8742-40be-9e7e-0b574ae38815
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 059c5bbe-07eb-4873-8157-2196df887b27
exl-id: 622cf6ca-f119-4310-ad14-537576bd6f6d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# Nozioni di base sui forum {#forum-essentials}

Questa pagina fornisce le informazioni essenziali per l&#39;utilizzo della funzione forum.

## Nozioni di base per lato client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceTypes</strong></td>
   <td>social/forum/components/hbs/forum<br /> social/forum/componenti/hbs/argomento<br /> social/forum/componenti/hbs/post</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluso</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.forum</td>
  </tr>
  <tr>
   <td> <strong>modelli</strong></td>
   <td> /libs/social/forum/components/hbs/forum/forum.hbs<br /> /libs/social/forum/components/hbs/post/post.hbs<br /> /libs/social/forum/components/hbs/topic/topic.hbs<br /> /libs/social/forum/components/hbs/topic/list-item.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/forum/components/hbs/forum/clientlibs/forum.css</td>
  </tr>
  <tr>
   <td><strong> proprietà</strong></td>
   <td>Consulta <a href="forum.md">Funzione forum</a></td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](client-customize.md)

## Nozioni di base per lato server {#essentials-for-server-side}

* [API forum](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/forum/client/api/package-summary.html)

* [Endpoint forum](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/forum/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Funzione Forum {#forum-function}

Una struttura del sito della community che include [Funzione forum](functions.md#forum-function), include un `forum` nonché le impostazioni relative a moderazione, assegnazione di tag e traduzione.

### Accesso ai post del forum (UGC) {#accessing-forum-posts-ugc}

Il contenuto UGC deve essere moderato utilizzando uno dei metodi standard per la moderazione.
Consulta [Moderazione dei contenuti generati dagli utenti](moderate-ugc.md).

A partire dalla AEM 6.1 Communities, l&#39;utilizzo di un [archivio comune](working-with-srp.md) per UGC include l’accesso programmatico a UGC indipendentemente dall’opzione di archiviazione scelta (ad esempio ASRP, MSRP o JSRP).

**La posizione e il formato dell’UGC nell’archivio sono soggetti a modifiche senza preavviso**.

Consulta:

* [Panoramica del provider di risorse di archiviazione](srp.md) - Introduzione e panoramica sull’utilizzo dell’archivio.
* [Nozioni di base su SRP e UGC](srp-and-ugc.md) - Metodi ed esempi di utilità SRP.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - Linee guida per la codifica.
* [Refactoring SocialUtils](socialutils.md) - Mappatura dei metodi di utilità obsoleti sui metodi di utilità SRP correnti.
