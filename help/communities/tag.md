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
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 3%

---

# Nozioni di base sui tag {#tag-essentials}

Quando i componenti AEM Communities sono configurati con l’assegnazione tag abilitata, i membri della community possono assegnare tag ai contenuti pubblicati nell’ambiente di pubblicazione.

L’infrastruttura sottostante per i tag applicati nell’ambiente di pubblicazione è la stessa dei tag applicati al contenuto nell’ambiente di authoring, ad esempio pagine e risorse:

* Vedi [Amministrazione dei tag](../../help/sites-administering/tags.md) e [Assegnazione tag ai contenuti generati dagli utenti](tag-ugc.md) (UGC) per informazioni sulla creazione e la gestione dei tag.

* Vedi [Assegnazione tag per sviluppatori](../../help/sites-developing/tags.md) per informazioni sulle [framework di assegnazione tag](../../help/sites-developing/framework.md) nonché l&#39;inclusione e l&#39;estensione dei tag in [applicazioni personalizzate](../../help/sites-developing/building.md).

* Vedi [Utilizzo di Social Tag Cloud](tagcloud.md) informazioni per gli autori su come aggiungere un `social tag cloud` per evidenziare i tag applicati a UGC nell’ambiente di pubblicazione.

* Vedi [Risorse di abilitazione assegnazione tag](tag-resources.md) per informazioni sull’assegnazione di tag alle risorse per i cataloghi.

Durante la configurazione di un [sito della community](sites-console.md#tagging) o una delle seguenti caratteristiche:

* [Blog](blog-feature.md)
* [Calendario](calendar.md)
* [Libreria file](file-library.md)
* [Forum](forum.md)
* [D/R](working-with-qna.md)

## Funzionalità di base per lato client {#essentials-for-client-side}

### Tag cloud per social network {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>comprensivo</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
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
   <td>Vedi <a href="tagcloud.md">Utilizzo di Social Tag Cloud</a></td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](client-customize.md)

## Funzioni di base per lato server {#essentials-for-server-side}

* [API per social tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [Social Tag Manager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

## Ricerca tag {#tag-searching}

A partire da [feature pack 1](deploy-communities.md#latestfeaturepack) (FP1), la ricerca tag viene eseguita utilizzando [titoli tag](../../help/sites-developing/framework.md#tag-characteristics).

Prima di FP1, la ricerca è stata eseguita utilizzando [id tag](../../help/sites-developing/framework.md#tagid).
