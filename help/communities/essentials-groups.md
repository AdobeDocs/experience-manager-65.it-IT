---
title: Nozioni di base sui gruppi community
seo-title: Community Group Essentials
description: Creazione dinamica di siti community
seo-description: Creating community sites dynamically
uuid: 168e7aeb-6e9a-468d-8ac4-274007cea252
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4f85cd3c-5158-4f23-abe2-7e375fd0c8d4
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 1%

---

# Nozioni di base sui gruppi community  {#community-group-essentials}

La funzione gruppi community consente a una sottocommunity di creare in modo dinamico all’interno di un sito community da parte di utenti autorizzati dagli ambienti di pubblicazione e authoring.

A livello di Comunità [feature pack 1](deploy-communities.md#latestfeaturepack), è possibile nidificare i gruppi all’interno di altri gruppi

## Funzionalità di base per lato client {#essentials-for-client-side}

### Elenco membri gruppi community {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/community/memberlist</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
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
   <td>Vedi <a href="creating-groups.md">Gruppo community</a></td>
  </tr>
 </tbody>
</table>

### Gruppi community {#community-groups}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/gruppo/componenti/hbs/community</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
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

## Funzioni di base per lato server {#essentials-for-server-side}

* [API gruppo community](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [Endpoint gruppo community](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Funzione Groups {#groups-function}

Una struttura del sito community che include una [Funzione Groups](functions.md#groups-function) sosterrà la creazione di nuovi `community groups` dagli ambienti di pubblicazione e authoring. Il gruppo comunitario creato includerà un `community groups member list` che elenca i membri del gruppo.

Uno o più [modelli di gruppo community](tools-groups.md), che forniscono la progettazione delle pagine del gruppo community, può essere configurato per la funzione Groups quando la funzione viene aggiunta a un [modello di sito community](sites.md) o nidificato all&#39;interno di un modello di gruppo community.

L&#39;inclusione di più modelli di gruppo community comporta la presentazione di una scelta di design all&#39;utente autorizzato al momento della creazione di un nuovo gruppo community per il sito community, come illustrato nella sezione [gruppi comunitari](creating-groups.md) per gli autori.

### Gruppi nidificati {#nested-groups}

A livello di Comunità [FP1](deploy-communities.md#latestfeaturepack), è possibile includere una funzione Groups all&#39;interno di un modello di gruppo, consentendo così ai gruppi nidificati (sottocomunità).

Quando un sito community o un modello di gruppo include la funzione Groups (Gruppi), è possibile:

* Crea una sottocommunity nell’ambiente di authoring.

* Crea un gruppo nell’ambiente di pubblicazione, se configurato per consentirlo.

Quando crei un gruppo nell&#39;ambiente di authoring, è necessario prima pubblicare il sito della community e poi pubblicare il gruppo. La pubblicazione del sito della community consente di pubblicare le pagine del gruppo senza creare i gruppi di membri della sottocomunità in cui sono impostate le ACL. Pertanto, un gruppo ristretto (segreto) può essere visibile fino a quando il gruppo non viene pubblicato esplicitamente.

## Collegamenti e informazioni correlate {#links-and-related-information}

* [Gestione di utenti e gruppi di utenti](users.md)
* [Console Gruppi community](groups.md)
* [Funzione Groups](functions.md#groups-function)
* [Modelli per gruppi](tools-groups.md)
