---
title: Tag Essentials
seo-title: Tag Essentials
description: Panoramica sui tag
seo-description: Panoramica sui tag
uuid: a5d52319-f821-4608-b0ab-abc8a1374343
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d355a3ee-c8a8-4a07-8d28-d1a99bda315c
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Tag Essentials {#tag-essentials}

Quando i componenti di AEM Communities sono configurati con l&#39;assegnazione di tag abilitata, i membri della community possono assegnare tag ai contenuti pubblicati nell&#39;ambiente di pubblicazione.

L’infrastruttura sottostante per i tag applicati nell’ambiente di pubblicazione è identica a quella per i tag applicati al contenuto nell’ambiente di authoring, ad esempio pagine e risorse:

* Per informazioni sulla creazione e la gestione dei tag, consultate [Amministrazione di tag](../../help/sites-administering/tags.md) e [assegnazione di tag ai contenuti](tag-ugc.md) generati dall’utente (UGC).

* See [Tagging for Developers](../../help/sites-developing/tags.md) for information about the [tagging framework](../../help/sites-developing/framework.md) as well as including and extending tags in [custom applications](../../help/sites-developing/building.md).

* Consultate [Utilizzo di Social Tag Cloud](tagcloud.md) per informazioni per gli autori su come aggiungere un `social tag cloud` componente a una pagina per evidenziare i tag applicati a UGC nell’ambiente di pubblicazione.

* Consultate [Assegnazione di tag alle risorse](tag-resources.md) di abilitazione per informazioni sui tag delle risorse per i cataloghi.

Quando si configura un sito [](sites-console.md#tagging) community o una delle seguenti funzioni, è possibile abilitare l&#39;assegnazione di tag UGC:

* [Blog](blog-feature.md)
* [Calendario](calendar.md)
* [Libreria file](file-library.md)
* [Forum](forum.md)
* [D/R](working-with-qna.md)

## Essentials for Client-Side {#essentials-for-client-side}

### Tag cloud per social network {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusa</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.tagcloud</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/tagcloud.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/clientlibs/tagcloud.css</td>
  </tr>
  <tr>
   <td><strong>proprietà</strong></td>
   <td>Consultate <a href="tagcloud.md">Utilizzo di Social Tag Cloud</a></td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API per social tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [Social Tag Manager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

## Ricerca tag {#tag-searching}

A partire dal [feature pack 1](deploy-communities.md#latestfeaturepack) (FP1), la ricerca tag viene eseguita utilizzando i titoli [](../../help/sites-developing/framework.md#tag-characteristics)dei tag.

Prima di FP1, la ricerca veniva eseguita utilizzando gli ID [](../../help/sites-developing/framework.md#tagid)tag.
