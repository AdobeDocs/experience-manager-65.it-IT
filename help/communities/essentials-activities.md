---
title: Nozioni di base sul flusso di attività
seo-title: Activity Stream Essentials
description: Elenco delle attività recenti eseguite da un membro o elenco delle attività recenti su un singolo thread di contenuto
seo-description: List of recent activites performed by a member or a list of recent activities on a single thread of content
uuid: 30c5ac08-0af0-4670-9d81-0beb5c93e00a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8714b456-527a-457b-82c4-21bd445dfd9c
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 2%

---

# Nozioni di base sul flusso di attività {#activity-stream-essentials}

Le attività di un membro della community firmato, come l’invio a un forum o blog, vengono raccolte in un flusso che può essere filtrato e visualizzato in vari modi tramite la configurazione del componente flussi di attività.

La possibilità di seguire aggiunge un altro insieme di attività quando i membri della comunità seguono post di interesse o altri membri della comunità.

Tutto [siti della community](/help/communities/overview.md#communitiessites) includere una pagina del profilo utente per il membro firmato che visualizzerà le attività membro nello stesso modo.

## Concetti {#concepts}

Un *flusso di attività* è l’elenco delle attività recenti eseguite da un membro o un elenco delle attività recenti relative a un singolo thread di contenuto, ad esempio un argomento del forum o un blog.

Un membro può seguire un flusso di attività seguendo un altro individuo o contenuto.

A *news feed* è un’unione dei flussi di attività seguiti da un membro in un singolo flusso.

A *[grafico sociale](/help/communities/essentials-socialgraph.md)* acquisisce le seguenti relazioni di un membro con un altro.

## Funzionalità di base per lato client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activitystream/components/hbs/activitystream</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>comprensivo</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.activitystreams</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/activitystreams.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity-title.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td>
  </tr>
  <tr>
   <td><strong> proprietà</strong></td>
   <td>Vedi <a href="/help/communities/activities.md">Funzionalità dei flussi di attività</a></td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](/help/communities/client-customize.md)

## Funzioni di base per lato server {#essentials-for-server-side}

* [API per flussi di attività](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [API del listener dei flussi di attività](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [Personalizzazioni lato server](/help/communities/server-customize.md)

### Funzione Flusso attività {#activity-stream-function}

Una struttura del sito community che include [Funzione Activity Stream](/help/communities/functions.md#activity-stream-function)include un `activity streams` componente.
