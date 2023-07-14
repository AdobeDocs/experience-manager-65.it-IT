---
title: Nozioni di base sul gruppo community
description: Creazione dinamica di siti community
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
source-git-commit: 681d1e6bd885b801b930e580d95645f160f17cea
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 1%

---

# Nozioni di base sul gruppo community  {#community-group-essentials}

La funzione Gruppi community consente la creazione dinamica di una sottocommunity all’interno di un sito community da parte di utenti autorizzati dagli ambienti di pubblicazione e authoring.

A partire da Communities [feature pack 1](deploy-communities.md#latestfeaturepack), è possibile nidificare i gruppi all’interno di altri gruppi

## Nozioni di base per lato client {#essentials-for-client-side}

### Elenco membri di gruppi community {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/communitygroupmemberlist</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>modelli</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/communitygroupmemberlist.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/memberList.css</td>
  </tr>
  <tr>
   <td><strong>proprietà</strong></td>
   <td>Consulta <a href="creating-groups.md">Gruppo community</a></td>
  </tr>
 </tbody>
</table>

### Gruppi community {#community-groups}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/community groups</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>modelli</strong></td>
   <td> /libs/social/group/components/hbs/communitygroups/communitygroups.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/communitygroups.css</td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](client-customize.md)

## Nozioni di base per lato server {#essentials-for-server-side}

* [API gruppo community](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [Endpoint gruppo community](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Funzione Gruppi {#groups-function}

Una struttura del sito della community che include [Funzione Gruppi](functions.md#groups-function) supporta la creazione di nuovi `community groups` dagli ambienti di pubblicazione e di authoring. Il gruppo community creato include `community groups member list` componente che elenca i membri del gruppo.

Uno o più [modelli per gruppi community](tools-groups.md), che forniscono la struttura delle pagine del gruppo community, possono essere configurate per la funzione Gruppi quando la funzione viene aggiunta a una [modello per sito community](sites.md) o nidificati all&#39;interno di un modello di gruppo community.

L&#39;inclusione di più modelli di gruppo community comporta la presentazione di una scelta di progetto all&#39;utente autorizzato al momento della creazione di un nuovo gruppo community per il sito community, come illustrato nella sezione relativa a [gruppi community](creating-groups.md) per autori.

### Gruppi nidificati {#nested-groups}

A partire da Communities [FP1](deploy-communities.md#latestfeaturepack), è possibile includere una funzione Gruppi all’interno di un modello di gruppo, consentendo in tal modo i gruppi nidificati (sottocomunità).

Quando un sito community o un modello di gruppo include la funzione Gruppi, è possibile:

* Crea una sottocommunity nell’ambiente di authoring.

* Crea un gruppo nell’ambiente di pubblicazione, se configurato per consentirlo.

Quando si crea un gruppo nell&#39;ambiente di authoring, è necessario innanzitutto pubblicare il sito della community e quindi pubblicare il gruppo. Quando si pubblica il sito community, le pagine del gruppo vengono pubblicate senza creare i gruppi di membri della sottocommunity ai quali sono impostati gli ACL. Pertanto, un gruppo ristretto (segreto) può essere visibile fino a quando non viene esplicitamente pubblicato.

## Collegamenti e informazioni correlate {#links-and-related-information}

* [Gestione di utenti e gruppi di utenti](users.md)
* [Console Gruppi community](groups.md)
* [Funzione Gruppi](functions.md#groups-function)
* [Modelli per gruppi](tools-groups.md)
