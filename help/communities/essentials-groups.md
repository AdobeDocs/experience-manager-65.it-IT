---
title: Community Group Essentials
seo-title: Community Group Essentials
description: Creazione dinamica di siti community
seo-description: Creazione dinamica di siti community
uuid: 168e7aeb-6e9a-468d-8ac4-274007cea252
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4f85cd3c-5158-4f23-abe2-7e375fd0c8d4
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 1%

---


# Elementi fondamentali del gruppo community {#community-group-essentials}

La funzione per i gruppi della community è la possibilità per una sottocomunità di essere creata in modo dinamico all&#39;interno di un sito della community da utenti autorizzati dagli ambienti di pubblicazione e authoring.

A partire da Communities [feature pack 1](deploy-communities.md#latestfeaturepack), è possibile che i gruppi siano nidificati all&#39;interno di altri gruppi

## Essentials for Client-Side {#essentials-for-client-side}

### Elenco membri gruppi community {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/community_memberlist</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/communitygroupmemberlist.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/memberList.css</td>
  </tr>
  <tr>
   <td><strong>proprietà</strong></td>
   <td>Vedere <a href="creating-groups.md">Gruppo community</a></td>
  </tr>
 </tbody>
</table>

### Gruppi community {#community-groups}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/community</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/group/components/hbs/communitygroups/communitygroups.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/communitygroups.css</td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API del gruppo community](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [Endpoint gruppo community](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Funzione dei gruppi {#groups-function}

Una struttura del sito della community che include una funzione [Groups](functions.md#groups-function) supporterà la creazione di nuove `community groups` dagli ambienti di pubblicazione e authoring. Il gruppo di community creato includerà un componente `community groups member list` che elenca i membri del gruppo.

È possibile configurare uno o più [modelli di gruppo community](tools-groups.md), che forniscono la progettazione delle pagine di gruppo community, per la funzione Groups quando la funzione viene aggiunta a un [modello di sito community](sites.md) o nidificata all&#39;interno di un modello di gruppo community.

L&#39;inclusione di più modelli di gruppo community comporta la presentazione di una scelta di progettazione all&#39;utente autorizzato al momento della creazione di un nuovo gruppo community per il sito community, come illustrato nella sezione relativa ai [gruppi community](creating-groups.md) per gli autori.

### Gruppi nidificati {#nested-groups}

Per quanto riguarda Community [FP1](deploy-communities.md#latestfeaturepack), è possibile includere una funzione Gruppi in un modello di gruppo, consentendo così l&#39;inclusione di gruppi nidificati (sub community).

Quando un sito o un modello di gruppo community include la funzione Groups, è possibile:

* Create una sub-community nell’ambiente di authoring.

* Create un gruppo nell’ambiente di pubblicazione, se configurato per consentirlo.

Quando create un gruppo nell’ambiente di authoring, è necessario prima pubblicare il sito della community, quindi pubblicarlo. La pubblicazione del sito della community consente di pubblicare le pagine del gruppo, senza creare i gruppi membri della sottocomunità ai quali sono impostati gli ACL. Pertanto, un gruppo con restrizioni (segreto) può essere visibile finché il gruppo non viene pubblicato in modo esplicito.

## Collegamenti e informazioni correlate {#links-and-related-information}

* [Gestione di utenti e gruppi di utenti](users.md)
* [Console Gruppi community](groups.md)
* [Funzione Groups](functions.md#groups-function)
* [Modelli per gruppi](tools-groups.md)

