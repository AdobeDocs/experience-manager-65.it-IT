---
title: Nozioni di base sui tag
seo-title: Tag Essentials
description: Panoramica sui tag
seo-description: Tag overview
uuid: a5d52319-f821-4608-b0ab-abc8a1374343
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d355a3ee-c8a8-4a07-8d28-d1a99bda315c
exl-id: 6e8af8cf-1239-46f9-b2fe-4aa80abc86ea
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 3%

---

# Nozioni di base sui tag {#tag-essentials}

Quando i componenti AEM Communities sono configurati con l’assegnazione tag abilitata, i membri della community possono assegnare tag ai contenuti pubblicati nell’ambiente di pubblicazione.

L’infrastruttura di base per i tag applicati nell’ambiente di pubblicazione è la stessa dei tag applicati al contenuto nell’ambiente di authoring, ad esempio pagine e risorse:

* Consulta [Amministrazione dei tag](../../help/sites-administering/tags.md) e [Assegnazione di tag ai contenuti generati dagli utenti](tag-ugc.md) (UGC) per informazioni sulla creazione e la gestione dei tag.

* Consulta [Assegnazione di tag per sviluppatori](../../help/sites-developing/tags.md) per informazioni su [framework di assegnazione tag](../../help/sites-developing/framework.md) nonché l’inclusione e l’estensione dei tag in [applicazioni personalizzate](../../help/sites-developing/building.md).

* Consulta [Utilizzo di Tag cloud per social network](tagcloud.md) per informazioni per gli autori su come aggiungere un `social tag cloud` a una pagina per evidenziare i tag applicati a UGC nell’ambiente di pubblicazione.

L’assegnazione tag di UGC può essere abilitata durante la configurazione di un [sito community](sites-console.md#tagging) oppure una delle seguenti caratteristiche:

* [Blog](blog-feature.md)
* [Calendario](calendar.md)
* [Libreria file](file-library.md)
* [Forum](forum.md)
* [D/R](working-with-qna.md)

## Nozioni di base per lato client {#essentials-for-client-side}

### Tag cloud per social network {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluso</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.tagcloud</td>
  </tr>
  <tr>
   <td> <strong>modelli</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/tagcloud.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/clientlibs/tagcloud.css</td>
  </tr>
  <tr>
   <td><strong>proprietà</strong></td>
   <td>Consulta <a href="tagcloud.md">Utilizzo di Tag cloud per social network</a></td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](client-customize.md)

## Nozioni di base per lato server {#essentials-for-server-side}

* [API tag cloud per social network](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [Gestione tag per social network](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

## Ricerca tag {#tag-searching}

A partire da [feature pack 1](deploy-communities.md#latestfeaturepack) (FP1), la ricerca dei tag viene eseguita utilizzando [titoli tag](../../help/sites-developing/framework.md#tag-characteristics).

Prima di FP1, la ricerca è stata eseguita utilizzando [id tag](../../help/sites-developing/framework.md#tagid).
