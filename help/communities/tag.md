---
title: Nozioni di base sui tag
description: Scopri quando i componenti Community sono configurati con l’assegnazione tag abilitata, i membri della community possono assegnare tag ai contenuti pubblicati nell’ambiente di pubblicazione.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 6e8af8cf-1239-46f9-b2fe-4aa80abc86ea
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 3%

---

# Nozioni di base sui tag {#tag-essentials}

Quando i componenti AEM Communities sono configurati con l’assegnazione tag abilitata, i membri della community possono assegnare tag ai contenuti pubblicati nell’ambiente di pubblicazione.

L’infrastruttura di base per i tag applicati nell’ambiente di pubblicazione è la stessa dei tag applicati al contenuto nell’ambiente di authoring, ad esempio pagine e risorse:

* Per informazioni sulla creazione e la gestione dei tag, vedere [Amministrazione dei tag](../../help/sites-administering/tags.md) e [Assegnazione dei tag ai contenuti generati dagli utenti](tag-ugc.md) (UGC).

* Consulta [Assegnazione tag per sviluppatori](../../help/sites-developing/tags.md) per informazioni sul [framework di assegnazione tag](../../help/sites-developing/framework.md) e sull&#39;inclusione e l&#39;estensione dei tag in [applicazioni personalizzate](../../help/sites-developing/building.md).

* Consulta [Utilizzo di Social Tag Cloud](tagcloud.md) per informazioni per gli autori su come aggiungere un componente `social tag cloud` a una pagina per evidenziare i tag applicati a UGC nell&#39;ambiente di pubblicazione.

L&#39;assegnazione tag di contenuti generati dagli utenti può essere abilitata durante la configurazione di un [sito community](sites-console.md#tagging) o di una delle seguenti funzionalità:

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
   <td> <strong>tiporisorsa</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>includibile</strong></a></td>
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
   <td>Vedi <a href="tagcloud.md">Utilizzo di Social Tag Cloud</a></td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](client-customize.md)

## Nozioni di base per lato server {#essentials-for-server-side}

* [API cloud per tag social network](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [Gestione tag social](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

## Ricerca tag {#tag-searching}

A partire dal [feature pack 1](deploy-communities.md#latestfeaturepack) (FP1), la ricerca dei tag viene eseguita utilizzando [titoli tag](../../help/sites-developing/framework.md#tag-characteristics).

Prima di FP1, la ricerca è stata eseguita utilizzando [ID tag](../../help/sites-developing/framework.md#tagid).
