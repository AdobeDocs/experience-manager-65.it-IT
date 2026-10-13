---
title: Nozioni di base sul flusso di attività
description: Elenco di attività recenti eseguite da un membro o un elenco di attività recenti su un singolo thread di contenuti
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 1%
---
# Nozioni di base sul flusso di attività {#activity-stream-essentials}

Le attività di un membro della community che ha effettuato l’accesso, ad esempio la pubblicazione in un forum o in un blog, vengono raccolte in un flusso che può essere filtrato e visualizzato in vari modi tramite la configurazione del componente Flussi di attività.

La possibilità di seguire aggiunge un altro set di attività quando i membri della community seguono postazioni di interesse o altri membri della community.

Tutti i [siti community](/help/communities/overview.md#communitiessites) includono una pagina del profilo utente per il membro connesso che visualizzerà le attività dei membri nello stesso modo.

## Concetti {#concepts}

Un *flusso di attività* è l&#39;elenco delle attività recenti eseguite da un membro o un elenco di attività recenti su un singolo thread di contenuti, ad esempio un argomento forum o un blog.

Un membro può seguire un flusso di attività, seguendo un altro individuo o un contenuto.

Un *feed di notizie* è un&#39;unione dei flussi di attività seguiti da un membro in un singolo flusso.

Un *[grafico social](/help/communities/essentials-socialgraph.md)* acquisisce le relazioni seguenti tra un membro e un altro.

## Nozioni di base per lato client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>tiporisorsa</strong></td>
   <td>social/activitystreams/components/hbs/activitystreams</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>includibile</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.activitystreams</td>
  </tr>
  <tr>
   <td> <strong>modelli</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/activitystreams.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity-title.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td>
  </tr>
  <tr>
   <td><strong> proprietà</strong></td>
   <td>Vedi la funzionalità <a href="/help/communities/activities.md">Flussi attività</a></td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](/help/communities/client-customize.md)

## Nozioni di base per lato server {#essentials-for-server-side}

* [API per flussi di attività](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [API del listener per flussi attività](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [Personalizzazioni lato server](/help/communities/server-customize.md)

### Funzione Flusso attività {#activity-stream-function}

Una struttura del sito della community che include la funzione [Flusso attività](/help/communities/functions.md#activity-stream-function) include un componente `activity streams` configurato.
