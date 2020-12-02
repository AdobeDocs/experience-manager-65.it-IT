---
title: Social Graph Essentials
seo-title: Social Graph Essentials
description: seguire la panoramica del componente e del componente seguente
seo-description: seguire la panoramica del componente e del componente seguente
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 4%

---


# Nozioni di base di grafico social network {#social-graph-essentials}

La capacità di un membro della Comunità di seguire [le attività](essentials-activities.md) e di seguirle è stabilita tramite due componenti:

Il componente `following` deve essere associato a un&#39;altra risorsa, e questa associazione è già stabilita per i membri e le funzioni Community esistenti in un [sito community](overview.md#communitiessites).

Il componente `following` elenca i membri che seguono il membro corrente o che sono seguiti dal membro corrente. Questo grafico social delle relazioni tra i membri è incluso nel profilo utente stabilito per un sito community.

## Essentials for Client-Side {#essentials-for-client-side}

### Segue {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/socialgrafo/componenti/hbs/relazioni</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusa</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.socialgraph</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/relationships.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/clientlibs/relationships.css</td>
  </tr>
  <tr>
   <td><strong> proprietà</strong></td>
   <td>Vedere <a href="socialgraph.md">Utilizzo di Social Graph</a></td>
  </tr>
  <tr>
   <td><strong> proprietà opzionale<br /></strong></td>
   <td>
    <ul>
     <li>Nome: <strong><code>outgoing</code></strong></li>
     <li>Tipo: booleano</li>
     <li>Valore:<br />
      <ul>
       <li><i>True  </i>- Il  <code>following</code> componente elenca i membri che hanno effettuato l'accesso <code>follows</code></li>
       <li><i>Falso  </i>- Il  <code>following</code> componente elenca i membri  <code>follow </code>del membro attualmente connesso</li>
      </ul> </li>
    </ul> <p>Il valore predefinito è <i>true</i> se la proprietà è mancante. Al momento, non è possibile impostare questa proprietà utilizzando la finestra di dialogo di modifica in modalità di creazione. La proprietà deve essere aggiunta a un'istanza del nodo <code>following </code>utilizzando <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Segui {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**inclusa**](scf.md#add-or-include-a-communities-component) | No |
| **templates** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [Personalizzazioni lato client](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API Grafico social](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [Endpoint grafico social](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [Personalizzazioni lato server](server-customize.md)

