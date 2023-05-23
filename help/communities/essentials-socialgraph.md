---
title: Nozioni di base sui grafici social
seo-title: Social Graph Essentials
description: segui la panoramica del componente e dei seguenti componenti
seo-description: follow component and following component overview
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
exl-id: c037a788-c943-4f95-a028-1fcb0ef48f86
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 2%

---

# Nozioni di base sui grafici social  {#social-graph-essentials}

Possibilità per un membro della community di seguire [attività](essentials-activities.md) L’eVar viene stabilito attraverso due componenti:

Il `following` il componente deve essere associato a un&#39;altra risorsa e questa associazione è già stata stabilita per i membri e le funzionalità delle community esistenti in un [sito community](overview.md#communitiessites).

Il `following` componente elenca i membri che seguono il membro corrente o che sono seguiti dal membro corrente. Questo grafico social delle relazioni tra i membri è incluso nel profilo utente stabilito per un sito community.

## Nozioni di base per lato client {#essentials-for-client-side}

### Segue {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/socialgraph/components/hbs/reports</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluso</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.socialgraph</td>
  </tr>
  <tr>
   <td> <strong>modelli</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/relationships.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/clientlibs/relationships.css</td>
  </tr>
  <tr>
   <td><strong> proprietà</strong></td>
   <td>Consulta <a href="socialgraph.md">Utilizzo di Social Graph</a></td>
  </tr>
  <tr>
   <td><strong> facoltativo<br /> proprietà</strong></td>
   <td>
    <ul>
     <li>Nome: <strong><code>outgoing</code></strong></li>
     <li>Tipo: booleano</li>
     <li>Valore:<br />
      <ul>
       <li><i>Vero </i>- Il <code>following</code> Il componente elencherà i membri che il membro attualmente connesso <code>follows</code></li>
       <li><i>Falso </i>- Il <code>following</code> il componente elencherà i membri che <code>follow </code>il membro attualmente connesso</li>
      </ul> </li>
    </ul> <p>Impostazione predefinita <i>true</i> se manca la proprietà. Attualmente, non è possibile impostare questa proprietà utilizzando la finestra di dialogo per modifica in modalità di authoring. La proprietà deve essere aggiunta a un’istanza di <code>following </code>nodo tramite <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Segui {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**incluso**](scf.md#add-or-include-a-communities-component) | No |
| **modelli** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [Personalizzazioni lato client](client-customize.md)

## Nozioni di base per lato server {#essentials-for-server-side}

* [API del grafico social network](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [Endpoint grafico social network](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [Personalizzazioni lato server](server-customize.md)
