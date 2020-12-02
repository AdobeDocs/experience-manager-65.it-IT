---
title: Nozioni di base sul flusso di attività
seo-title: Nozioni di base sul flusso di attività
description: Elenco delle attività recenti eseguite da un membro o elenco delle attività recenti su un singolo thread di contenuto
seo-description: Elenco delle attività recenti eseguite da un membro o elenco delle attività recenti su un singolo thread di contenuto
uuid: 30c5ac08-0af0-4670-9d81-0beb5c93e00a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8714b456-527a-457b-82c4-21bd445dfd9c
docset: aem65
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 2%

---


# Nozioni di base sul flusso di attività {#activity-stream-essentials}

Le attività di un membro della comunità firmato, come l&#39;invio a un forum o blog, vengono raccolte in un flusso che può essere filtrato e visualizzato in vari modi attraverso la configurazione del componente Flussi di attività.

La possibilità di seguire aggiunge un altro gruppo di attività quando i membri della comunità seguono postazioni di interesse o altri membri della comunità.

Tutti i [siti della community](/help/communities/overview.md#communitiessites) includono una pagina del profilo utente per il membro che ha effettuato l&#39;accesso e che mostrerà le attività dei membri allo stesso modo.

## Concetti {#concepts}

Un *flusso di attività* è l&#39;elenco delle attività recenti eseguite da un membro o un elenco delle attività recenti su un singolo thread di contenuto, ad esempio un topic o un blog.

Un membro può seguire un flusso di attività, seguendo un altro individuo o contenuto.

Un *feed di notizie* è un&#39;unione dei flussi di attività seguiti da un membro in un singolo flusso.

Un *[grafico sociale](/help/communities/essentials-socialgraph.md)* acquisisce le seguenti relazioni di un membro a un altro.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activitystreams/components/hbs/activitystream</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>inclusa</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
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
   <td>Vedere <a href="/help/communities/activities.md">Activity Streams Feature</a></td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](/help/communities/client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API Activity Streams](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [API Listener flussi di attività](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [Personalizzazioni lato server](/help/communities/server-customize.md)

### Funzione Flusso attività {#activity-stream-function}

Una struttura del sito community che include la funzione [Activity Stream](/help/communities/functions.md#activity-stream-function), include un componente `activity streams` configurato.
